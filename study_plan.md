# 45강 주차별 학습 체크리스트

이 문서는 `README.md`의 전체 학습 로드맵을 실습용 체크리스트로 옮긴 실행 문서입니다.

## 1. 사용 방법

- 한 주에 5강씩 진행합니다. (`9주 x 5강 = 45강`)
- 각 강의는 아래 순서로 실행합니다.
- `curriculum/lectureNN/README.md` 확인
- `curriculum/lectureNN/playbook.yml` 실행
- 실행 로그 1개 + 회고 노트 1개 저장

## 2. 공통 실행 루틴

```bash
# 강의 실행
ansible-playbook -i inventories/local/hosts.ini curriculum/lectureNN/playbook.yml

# 설치 태스크 포함 실행(필요 시)
ansible-playbook -i inventories/local/hosts.ini curriculum/lectureNN/playbook.yml -e install_enabled=true
```

## 3. 주차별 계획

## Week 1 (lecture01~lecture05)

- [ ] lecture01 Ansible 학습환경 진단과 컨트롤 노드 준비
- [ ] lecture02 Inventory 구조와 host/group 변수 설계
- [ ] lecture03 Ad-hoc 명령과 연결 테스트 자동화
- [ ] lecture04 변수, facts, register 실습
- [ ] lecture05 loop, when, block 제어문 실습
- [ ] 실행 로그 5개 이상 수집
- [ ] 회고 노트 5개 작성

## Week 2 (lecture06~lecture10)

- [ ] lecture06 Jinja2 템플릿과 설정 파일 생성
- [ ] lecture07 handler와 idempotency 검증
- [ ] lecture08 Role 구조 분해와 재사용 설계
- [ ] lecture09 공통 서버 부트스트랩 자동화
- [ ] lecture10 사용자/권한/SSH 정책 자동화
- [ ] 실행 로그 5개 이상 수집
- [ ] 회고 노트 5개 작성

## Week 3 (lecture11~lecture15)

- [ ] lecture11 Nginx 설치와 웹 서비스 배포 자동화
- [ ] lecture12 Docker Engine 설치 자동화
- [ ] lecture13 Compose 스택 배포 자동화
- [ ] lecture14 Rolling Update 배포 실습
- [ ] lecture15 Blue/Green 전환 자동화
- [ ] 운영 자동화 태스크 재실행으로 idempotency 확인
- [ ] 회고 노트 5개 작성

## Week 4 (lecture16~lecture20)

- [ ] lecture16 Trivy 기반 컨테이너 취약점 점검
- [ ] lecture17 Docker Bench 점검과 보고서 자동화
- [ ] lecture18 CrowdSec + Nginx 보안 실습 자동화
- [ ] lecture19 AWS SSM 기반 무SSH 프로비저닝
- [ ] lecture20 AWS VPC 네트워크 생성 자동화
- [ ] 보안/클라우드 체크리스트 정리
- [ ] 회고 노트 5개 작성

## Week 5 (lecture21~lecture25)

- [ ] lecture21 AWS EC2 인스턴스 생성 자동화
- [ ] lecture22 생성 후 SSM 기반 후속 설정 자동화
- [ ] lecture23 S3 버킷 생성/정책 자동화
- [ ] lecture24 AWS 출력값 수집과 결과 정리
- [ ] lecture25 AWS 실습 자원 정리 자동화
- [ ] AWS 생성/정리 전체 플로우 1회 재검증
- [ ] 회고 노트 5개 작성

## Week 6 (lecture26~lecture30)

- [ ] lecture26 Linux 운영 기본기: 프로세스/로그/서비스
- [ ] lecture27 VirtualBox 네트워크: NAT/Host-only/Bridged
- [ ] lecture28 Docker 기초: 이미지/컨테이너/레지스트리
- [ ] lecture29 백엔드 컨테이너 실행 흐름 이해
- [ ] lecture30 프론트엔드 정적 배포와 Nginx 연동
- [ ] Linux/네트워크 핵심 명령어 정리
- [ ] 회고 노트 5개 작성

## Week 7 (lecture31~lecture35)

- [ ] lecture31 Docker 네트워크/볼륨/데이터 영속성
- [ ] lecture32 멀티서비스 Compose 운영 패턴
- [ ] lecture33 k3s 아키텍처와 Kubernetes 핵심 리소스
- [ ] lecture34 k3s 서버 노드 준비 자동화 설계
- [ ] lecture35 k3s 에이전트 조인 자동화 설계
- [ ] Docker/k8s는 개요/연결 중심으로 최소 실습
- [ ] 회고 노트 5개 작성

## Week 8 (lecture36~lecture40)

- [ ] lecture36 Deployment/Service 선언형 배포 실습
- [ ] lecture37 Ingress와 외부 트래픽 라우팅
- [ ] lecture38 클러스터 로그/상태 관측 기초
- [ ] lecture39 OpenStack Neutron 네트워크 개념 매핑
- [ ] lecture40 Horizon 콘솔 운영 흐름과 IAM 관점
- [ ] AWS-OpenStack 리소스 매핑표 작성
- [ ] 회고 노트 5개 작성

## Week 9 (lecture41~lecture45)

- [ ] lecture41 로컬 실습과 AWS EC2/VPC/SG 매핑
- [ ] lecture42 ECR/ECS/EKS/IaC 확장 전략 수립
- [ ] lecture43 OpenStack 입문 1: MicroStack으로 Horizon과 첫 VM 체험
- [ ] lecture44 OpenStack 입문 2: DevStack 단일 머신 학습 흐름
- [ ] lecture45 OpenStack 입문 3: Kolla Ansible(Docker) 배포 방식 비교
- [ ] OpenStack 3방식 비교표(MicroStack/DevStack/Kolla) 작성
- [ ] 최종 회고 노트 작성

## 4. 최종 완료 체크

- [ ] 45개 강의 실행 완료
- [ ] 강의별 실행 로그 또는 스크린샷 확보
- [ ] 강의별 회고 노트 완료
- [ ] AWS/OpenStack 리소스 매핑 설명 가능
- [ ] 다음 심화 트랙 우선순위 결정 (`12-1` ~ `12-8`)

