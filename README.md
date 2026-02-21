# Python Ansible Playbook

이 저장소는 **Ansible 기반 인프라/애플리케이션 운영 자동화 예시**를 담고 있습니다.  
단순 Ping부터 시작해 Docker 엔진 표준 설치, Compose 배포, Rolling/Blue-Green 배포, AWS SSM(SSH 없이 운영)까지 실습할 수 있도록 구성되어 있습니다.

## 1) 이 프로젝트로 할 수 있는 것

- Inventory 기반으로 환경(dev/stage/prod, local/docker/aws) 분리 운영
- Role 중심으로 재사용 가능한 자동화 구성
- Docker Engine 설치 자동화
- Docker Compose 스택 배포 및 점진적(rolling) 배포
- Blue-Green 방식 배포 전환
- AWS 리소스 프로비저닝 + SSM 접속 기반 후속 작업(SSH 미사용)
- Trivy/Docker Bench/CrowdSec 기반 보안 점검 실험

## 2) 디렉터리 구조(핵심)

```text
.
├─ ansible.cfg
├─ inventories/
│  ├─ dev|stage|prod|local|docker|aws
├─ group_vars/
├─ playbooks/
│  ├─ 00_ping.yml
│  ├─ 10_docker_engine_install.yml
│  ├─ 11_deploy_stack.yml
│  ├─ 12_deploy_stack_rolling.yml
│  ├─ 13_blue_green_switch.yml
│  ├─ 20_aws_provision_ssm_no_ssh.yml
│  ├─ 21_post_provision_via_ssm.yml
│  ├─ 23_aws_cleanup.yml
│  ├─ 91_trivy_scan.yml / 92_docker_bench.yml / 93_crowdsec_nginx_lab.yml
├─ roles/
│  ├─ common / docker_engine / webserver / compose_stack / compose_blue_green
│  ├─ aws_ssm_provision / aws_ssm_cleanup
├─ stacks/
└─ docs/
```

## 3) 사전 준비

- Python 3.9+
- Ansible (ansible-core)
- (선택) AWS 실습 시 AWS 인증 정보
- (선택) Docker 관련 실습 시 대상 호스트 접근 권한

의존성 설치:

```bash
pip install -r requirements.txt
ansible-galaxy collection install -r requirements.yml
```

기본 설정 파일(`ansible.cfg`)에는 기본 inventory, roles path, SSH 최적화 옵션이 포함되어 있습니다.

## 4) 빠른 시작 (로컬 검증 루트)

### 4-1. 연결 확인

```bash
ansible-playbook -i inventories/dev/hosts.ini playbooks/00_ping.yml
```

### 4-2. Docker 엔진 설치

```bash
ansible-playbook -i inventories/dev/hosts.ini playbooks/10_docker_engine_install.yml
```

### 4-3. Compose 스택 배포

```bash
ansible-playbook -i inventories/dev/hosts.ini playbooks/11_deploy_stack.yml
```

## 5) 운영 배포 예시 (고도화)

### A. Rolling 배포 (호스트 1대씩)

서비스 중단 리스크를 줄이기 위해 `serial: 1`로 순차 배포합니다.

```bash
ansible-playbook -i inventories/prod/hosts.ini playbooks/12_deploy_stack_rolling.yml
```

### B. Blue-Green 배포

단일 호스트 기준으로 blue/green 슬롯 전환형 배포를 수행합니다.

```bash
ansible-playbook -i inventories/prod/hosts.ini playbooks/13_blue_green_switch.yml
```

### C. AWS SSM 기반(SSH 없이)

1) 인프라 + EC2 생성:

```bash
ansible-playbook playbooks/20_aws_provision_ssm_no_ssh.yml -e aws_region=ap-northeast-2 -e environment=dev
```

2) SSM 연결로 Docker/배포 후속 작업:

```bash
ansible-playbook -i inventories/aws/aws_ec2.yml playbooks/21_post_provision_via_ssm.yml -e aws_region=ap-northeast-2
```

3) 리소스 정리:

```bash
ansible-playbook playbooks/23_aws_cleanup.yml -e aws_region=ap-northeast-2 -e environment=dev
```

## 6) 기술 포인트 (실무 관점)

### 6-1. Role 기반 모듈화

- Playbook은 “오케스트레이션”, Role은 “실제 구현” 책임으로 분리
- 예: `docker_engine`, `compose_stack`, `compose_blue_green`, `aws_ssm_provision`

### 6-2. 환경 분리 전략

- Inventory를 환경 단위로 분리하여 동일 Playbook 재사용
- `group_vars`로 공통/환경별 변수 관리

### 6-3. 연결 방식 다변화

- 일반 SSH 연결 + AWS SSM 연결을 모두 지원
- 보안 요구사항에 따라 SSH 비활성 운영 시나리오로 확장 가능

### 6-4. 멱등성(Idempotency)

- Ansible 모듈/Role 구조를 통해 여러 번 실행해도 상태 수렴
- 운영 시 재실행 안전성을 높여 장애 복구 자동화에 유리

### 6-5. 보안 점검 자동화

- Trivy 이미지 취약점 스캔
- Docker Bench 결과 수집/리포트
- CrowdSec + Nginx 로그 기반 보안 실험

## 7) 자주 쓰는 실행 명령 모음

```bash
# ad-hoc ping
ansible -i inventories/dev/hosts.ini all -m ping

# inventory 구조 확인(AWS dynamic inventory)
ansible-inventory -i inventories/aws/aws_ec2.yml --graph

# 문법 점검
ansible-playbook -i inventories/dev/hosts.ini playbooks/11_deploy_stack.yml --syntax-check

# 체크 모드(변경 없이 드라이런)
ansible-playbook -i inventories/dev/hosts.ini playbooks/11_deploy_stack.yml --check
```

## 8) 문서 로드맵

처음 보는 경우 아래 순서로 읽는 것을 권장합니다.

1. `docs/00_overview.md`
2. `docs/00_prereqs.md`
3. `docs/01_ansible_basics.md`
4. `docs/02_roles_and_templates.md`
5. `docs/03_docker_with_ansible.md`
6. `docs/09_docker_management.md`
7. `docs/10_ci_cd.md`

## 9) 개발 편의 명령

```bash
make bootstrap
make lint
make inventory-aws
make molecule
```

> `molecule`/`ansible-lint`는 로컬 환경에 따라 추가 의존성이 필요할 수 있습니다.
