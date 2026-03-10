# lecture28 - Docker 기초: 이미지/컨테이너/레지스트리

## 1. 강의 개요
- 강의 번호: `28`
- 모듈: `Module D / Infra & Docker Fundamentals`
- 난이도: `beginner`
- 권장 시간: `120분`
- 모듈 초점: Linux/가상화 기반 이해가 중심이며 Docker는 최소 체험 범위로 운영합니다.

## 2. 선수 조건
- lecture27 완료 또는 동등한 실무 경험
- Linux 기본 명령어(ls, cat, systemctl) 사용 가능

## 3. 학습 목표
- Docker 기초: 이미지/컨테이너/레지스트리 주제를 Ansible 중심으로 설명할 수 있다.
- 강의별 설치 및 점검 절차를 YAML 문서 기반으로 수행할 수 있다.
- 실습 결과를 AI 코치 프롬프트로 리뷰하고 개선할 수 있다.

## 4. 기술 스택 반영
### 핵심 스택 (Primary)
- `ubuntu`
- `linux-cli`
- `networking`

### 보조 스택 (Secondary)
- `docker`

### 선택 스택
- `virtualbox`
- `vagrant`
- `tmux`

### 적용 원칙
- Docker/k8s 관련 항목은 개념 연결과 최소 실습 중심으로 진행합니다. 핵심 평가는 Ansible 자동화 문서화, 클라우드 매핑 이해, 재현 가능한 실행 절차에 둡니다.

## 5. 학습 구성
### 이론
- 핵심 개념 30분: 정의, 동작 원리, 실패 패턴
- 구조 이해 20분: 현재 리포 파일/디렉터리 매핑

### 실습
- 실습 50분: lecture playbook 실행 및 결과 검증
- 회고 20분: AI와 함께 오류 원인/개선안 정리

## 6. 설치 계획
- 대상 인벤토리: `../../inventories/local/hosts.ini`
- 대상 호스트 그룹: `all`
### 설치 접근
- 사전 점검: Python/SSH/권한 확인
- 필수 패키지 설치는 playbook.yml에서 install_enabled=true일 때 실행
- 강의 종료 후 상태 점검 태스크로 검증
### 패키지
- `python3`
- `curl`
- `jq`
- `net-tools`
- `unzip`

## 7. 실행 절차
- 강의 플레이북: `./playbook.yml`
- 레퍼런스 플레이북: `../../playbooks/10_docker_install.yml`
### 실행 명령
- `ansible-playbook -i ../../inventories/local/hosts.ini ./playbook.yml`
- `ansible-playbook -i ../../inventories/local/hosts.ini ./playbook.yml -e install_enabled=true`
- `ansible-playbook -i ../../inventories/local/hosts.ini ../../playbooks/10_docker_install.yml`

## 8. 산출물과 검증
### 산출물
- 강의 실행 로그 또는 스크린샷 1개 이상
- AI 회고 노트(markdown) 1개
### 검증 기준
- playbook syntax error 없음
- 핵심 태스크 결과를 debug 출력으로 확인

## 9. AI 페어링 가이드
- 사전 점검 프롬프트: Docker 기초: 이미지/컨테이너/레지스트리 실습 전에 실패할 수 있는 지점 3개를 체크리스트로 만들어줘.
- 실습 중 프롬프트: 현재 실행 로그를 보고 원인-증상-조치 순서로 트러블슈팅 가이드를 작성해줘.
- 회고 프롬프트: 이번 강의에서 배운 자동화 패턴을 다음 강의에 재사용할 수 있게 YAML 템플릿으로 정리해줘.

## 10. 심화 연계 (선택)
- 연계 트랙: `Docker Compose 추가`
- 연계 목표: Docker 기초: 이미지/컨테이너/레지스트리 학습 결과를 Docker Compose 추가 확장 시나리오와 연결한다.
### 추가 실습
- frontend + backend + postgres + redis 구성
- 서비스 간 네트워크 및 의존관계 확인
- AWS/OpenStack 브릿지: Compose 정의는 ECS Task 또는 Kubernetes 다중 리소스 분리 전 단계
- 확장 프롬프트: 현재 강의(Docker 기초: 이미지/컨테이너/레지스트리) 결과를 Docker Compose 추가 실습으로 확장하는 체크리스트를 YAML로 작성해줘.

## 11. 참고 파일
- `lecture.yml`: 강의 메타데이터
- `playbook.yml`: 강의 실행 플레이북

---
이 문서는 `lecture.yml`을 기준으로 생성된 강의 안내서입니다.
