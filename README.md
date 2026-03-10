# Python Ansible Playbook: Ansible-First 45 Lecture Curriculum

이 저장소는 **Ansible를 먼저 익히고**, 이후 Docker, k3s, AWS/OpenStack 개념으로 확장하는 실습형 학습 저장소입니다.

핵심은 다음 3가지입니다.

- `lecture01~lecture45`까지 단계형 커리큘럼
- 각 강의 폴더에 `lecture.yml` + `playbook.yml` 제공
- AI 보조 프롬프트를 활용한 실습/회고 루프

## 1. 학습 목표

- 반복되는 서버 작업을 Ansible Playbook으로 자동화한다.
- Docker/k3s/AWS 실습을 Ansible 기반 운영 관점으로 연결한다.
- YAML 문서 중심으로 설치/검증/회고를 일관되게 진행한다.

## 2. 저장소 구조

```text
Python_Ansible-Playbook/
├── README.md
├── ansible.cfg
├── requirements.txt
├── requirements.yml
├── inventories/
│   ├── local/
│   ├── dev/
│   ├── stage/
│   ├── prod/
│   └── aws/
├── group_vars/
├── playbooks/
│   ├── 00_ping.yml
│   ├── 00_bootstrap.yml
│   ├── 01_users.yml
│   ├── 02_nginx.yml
│   ├── 03_role_web.yml
│   ├── 10_docker_install.yml
│   ├── 10_docker_engine_install.yml
│   ├── 11_docker_run_nginx.yml
│   ├── 11_deploy_stack.yml
│   ├── 12_deploy_stack_rolling.yml
│   ├── 13_blue_green_switch.yml
│   ├── 20_aws_provision_ssm_no_ssh.yml
│   ├── 20_aws_create_vpc.yml
│   ├── 21_aws_create_ec2.yml
│   ├── 21_post_provision_via_ssm.yml
│   ├── 22_aws_s3_bucket.yml
│   ├── 23_aws_cleanup.yml
│   ├── 91_trivy_scan.yml
│   ├── 92_docker_bench.yml
│   ├── 93_crowdsec_nginx_lab.yml
│   └── learning/
├── roles/
├── stacks/
├── docs/
└── curriculum/
    ├── learning_path.yml
    ├── lecture01/
    │   ├── lecture.yml
    │   └── playbook.yml
    ├── ...
    └── lecture45/
        ├── lecture.yml
        └── playbook.yml
```

## 3. 커리큘럼 운영 원칙

- **Ansible 선행**: lecture01~25를 Ansible 중심으로 먼저 배치
- **YAML 중심**: 강의 정의/설치/실습은 `lecture.yml`에 명시
- **실행 파일 분리**: 강의 실행용 `playbook.yml`과 기존 레퍼런스 플레이북을 병행
- **AI 페어링**: 모든 강의에 `ai_pairing` 프롬프트 포함

## 4. 45강 모듈 구성

| Lecture Range | Module | Outcome |
|---|---|---|
| lecture01-lecture10 | Ansible Foundation | 인벤토리/변수/템플릿/Role 기반 자동화 기초 완성 |
| lecture11-lecture18 | Ansible Operations | 웹/컨테이너/보안 자동화 운영 패턴 습득 |
| lecture19-lecture25 | AWS Automation with Ansible | SSM/VPC/EC2/S3 생성과 정리 자동화 |
| lecture26-lecture32 | Infra & Docker Fundamentals | Linux/VirtualBox/Docker 실행 기반 이해 |
| lecture33-lecture38 | k3s & Kubernetes Operations | k3s 구조와 배포/관측 패턴 이해 |
| lecture39-lecture42 | Cloud Mapping | OpenStack/AWS 개념 매핑 |
| lecture43-lecture45 | Capstone | 통합 배포 리허설 + 운영 Runbook 완성 |

## 5. 강의별 파일 규칙

각 `curriculum/lectureNN/` 폴더는 아래 파일로 구성됩니다.

- `lecture.yml`: 학습 목표, 기술 스택, 설치 방안, AI 프롬프트, 참조 플레이북
- `playbook.yml`: 강의 실습용 Ansible Playbook

예시: `curriculum/lecture12/`

- `lecture.yml` → Docker Engine 설치 자동화 학습 설계
- `playbook.yml` → 강의용 설치/검증 태스크

## 6. 빠른 시작

### 6.1 의존성 설치

```bash
pip install -r requirements.txt
ansible-galaxy install -r requirements.yml
```

### 6.2 첫 강의 실행

```bash
ansible-playbook -i inventories/local/hosts.ini curriculum/lecture01/playbook.yml
```

실제 설치까지 수행하려면:

```bash
ansible-playbook -i inventories/local/hosts.ini curriculum/lecture01/playbook.yml -e install_enabled=true
```

### 6.3 강의 레퍼런스 플레이북 실행

각 강의의 `lecture.yml -> ansible_lab.reference_playbook` 경로를 사용합니다.

```bash
ansible-playbook -i inventories/local/hosts.ini playbooks/00_ping.yml
```

## 7. 전체 학습 진행 방법

1. `curriculum/learning_path.yml`에서 강의 순서 확인
2. `curriculum/lectureNN/lecture.yml`로 목표/설치/검증 기준 확인
3. `curriculum/lectureNN/playbook.yml` 실행
4. `ai_pairing` 프롬프트로 트러블슈팅/회고 정리
5. 필요 시 `reference_playbook` 실행으로 실전 플레이북과 연결

## 8. 45개 Lecture 목록

### Module A: Ansible Foundation (01-10)

- lecture01: Ansible 학습환경 진단과 컨트롤 노드 준비
- lecture02: Inventory 구조와 host/group 변수 설계
- lecture03: Ad-hoc 명령과 연결 테스트 자동화
- lecture04: 변수, facts, register 실습
- lecture05: loop, when, block 제어문 실습
- lecture06: Jinja2 템플릿과 설정 파일 생성
- lecture07: handler와 idempotency 검증
- lecture08: Role 구조 분해와 재사용 설계
- lecture09: 공통 서버 부트스트랩 자동화
- lecture10: 사용자/권한/SSH 정책 자동화

### Module B: Ansible Operations (11-18)

- lecture11: Nginx 설치와 웹 서비스 배포 자동화
- lecture12: Docker Engine 설치 자동화
- lecture13: Compose 스택 배포 자동화
- lecture14: Rolling Update 배포 실습
- lecture15: Blue/Green 전환 자동화
- lecture16: Trivy 기반 컨테이너 취약점 점검
- lecture17: Docker Bench 점검과 보고서 자동화
- lecture18: CrowdSec + Nginx 보안 실습 자동화

### Module C: AWS Automation with Ansible (19-25)

- lecture19: AWS SSM 기반 무SSH 프로비저닝
- lecture20: AWS VPC 네트워크 생성 자동화
- lecture21: AWS EC2 인스턴스 생성 자동화
- lecture22: 생성 후 SSM 기반 후속 설정 자동화
- lecture23: S3 버킷 생성/정책 자동화
- lecture24: AWS 출력값 수집과 결과 정리
- lecture25: AWS 실습 자원 정리 자동화

### Module D: Infra & Docker Fundamentals (26-32)

- lecture26: Linux 운영 기본기: 프로세스/로그/서비스
- lecture27: VirtualBox 네트워크: NAT/Host-only/Bridged
- lecture28: Docker 기초: 이미지/컨테이너/레지스트리
- lecture29: 백엔드 컨테이너 실행 흐름 이해
- lecture30: 프론트엔드 정적 배포와 Nginx 연동
- lecture31: Docker 네트워크/볼륨/데이터 영속성
- lecture32: 멀티서비스 Compose 운영 패턴

### Module E: k3s & Kubernetes Operations (33-38)

- lecture33: k3s 아키텍처와 Kubernetes 핵심 리소스
- lecture34: k3s 서버 노드 준비 자동화 설계
- lecture35: k3s 에이전트 조인 자동화 설계
- lecture36: Deployment/Service 선언형 배포 실습
- lecture37: Ingress와 외부 트래픽 라우팅
- lecture38: 클러스터 로그/상태 관측 기초

### Module F: Cloud Mapping (39-42)

- lecture39: OpenStack Neutron 네트워크 개념 매핑
- lecture40: Horizon 콘솔 운영 흐름과 IAM 관점
- lecture41: 로컬 실습과 AWS EC2/VPC/SG 매핑
- lecture42: ECR/ECS/EKS/IaC 확장 전략 수립

### Module G: Capstone (43-45)

- lecture43: 통합 아키텍처 설계 워크숍
- lecture44: 통합 배포 리허설과 장애 대응
- lecture45: 최종 캡스톤: 운영 Runbook 완성

## 9. 검증 체크 명령

```bash
find curriculum -maxdepth 1 -type d -name 'lecture*' | wc -l
find curriculum -maxdepth 2 -type f -name 'lecture.yml' | wc -l
find curriculum -maxdepth 2 -type f -name 'playbook.yml' | wc -l
```

기대값은 각각 `45`, `45`, `45`입니다.
