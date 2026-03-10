# lecture16 - Trivy 기반 컨테이너 취약점 점검

## 1. 강의 개요
- 강의 번호: `16`
- 모듈: `Module B / Ansible Operations`
- 난이도: `intermediate`
- 권장 시간: `120분`
- 모듈 초점: 운영 작업 자동화를 중심으로 실습하며 Docker는 보조 도구로 다룹니다.

## 2. 선수 조건
- lecture15 완료 또는 동등한 실무 경험
- Linux 기본 명령어(ls, cat, systemctl) 사용 가능

## 3. 학습 목표
- Trivy 기반 컨테이너 취약점 점검 주제를 Ansible 중심으로 설명할 수 있다.
- 강의별 설치 및 점검 절차를 YAML 문서 기반으로 수행할 수 있다.
- 실습 결과를 AI 코치 프롬프트로 리뷰하고 개선할 수 있다.

## 4. 기술 스택 반영
### 핵심 스택 (Primary)
- `ansible-core`
- `nginx`

### 보조 스택 (Secondary)
- `docker`
- `compose`

### 선택 스택
- `trivy`
- `docker-bench-security`
- `crowdsec`

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
- 대상 호스트 그룹: `docker`
### 설치 접근
- 사전 점검: Python/SSH/권한 확인
- 필수 패키지 설치는 playbook.yml에서 install_enabled=true일 때 실행
- 강의 종료 후 상태 점검 태스크로 검증
### 패키지
- `python3`
- `docker.io`
- `docker-compose-plugin`
- `nginx`
- `curl`

## 7. 실행 절차
- 강의 플레이북: `./playbook.yml`
- 레퍼런스 플레이북: `../../playbooks/91_trivy_scan.yml`
### 실행 명령
- `ansible-playbook -i ../../inventories/local/hosts.ini ./playbook.yml`
- `ansible-playbook -i ../../inventories/local/hosts.ini ./playbook.yml -e install_enabled=true`
- `ansible-playbook -i ../../inventories/local/hosts.ini ../../playbooks/91_trivy_scan.yml`

## 8. 산출물과 검증
### 산출물
- 강의 실행 로그 또는 스크린샷 1개 이상
- AI 회고 노트(markdown) 1개
### 검증 기준
- playbook syntax error 없음
- 핵심 태스크 결과를 debug 출력으로 확인

## 9. AI 페어링 가이드
- 사전 점검 프롬프트: Trivy 기반 컨테이너 취약점 점검 실습 전에 실패할 수 있는 지점 3개를 체크리스트로 만들어줘.
- 실습 중 프롬프트: 현재 실행 로그를 보고 원인-증상-조치 순서로 트러블슈팅 가이드를 작성해줘.
- 회고 프롬프트: 이번 강의에서 배운 자동화 패턴을 다음 강의에 재사용할 수 있게 YAML 템플릿으로 정리해줘.

## 10. 심화 연계 (선택)
- 연계 트랙: `모니터링(Prometheus/Grafana) 추가`
- 연계 목표: Trivy 기반 컨테이너 취약점 점검 학습 결과를 모니터링(Prometheus/Grafana) 추가 확장 시나리오와 연결한다.
### 추가 실습
- k3s에 Prometheus/Grafana 배포
- 응답시간/에러율 시각화
- AWS/OpenStack 브릿지: CloudWatch, Managed Prometheus, Managed Grafana와 연결 가능
- 확장 프롬프트: 현재 강의(Trivy 기반 컨테이너 취약점 점검) 결과를 모니터링(Prometheus/Grafana) 추가 실습으로 확장하는 체크리스트를 YAML로 작성해줘.

## 11. 참고 파일
- `lecture.yml`: 강의 메타데이터
- `playbook.yml`: 강의 실행 플레이북

---
이 문서는 `lecture.yml`을 기준으로 생성된 강의 안내서입니다.
