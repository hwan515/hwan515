# 👨‍💻 Hello! I'm Jihwan 🚀

Backend / Infra / AI / MLOps

운영 가능한 백엔드, 실시간 시스템, 배포 자동화, 모니터링을 중심으로 학습하고 구현합니다.

<p>
  <a href="https://github.com/hwan515">
    <img src="https://img.shields.io/badge/GitHub-hwan515-181717?style=flat-square&logo=github&logoColor=white" alt="GitHub hwan515" />
  </a>
  <a href="https://solved.ac/profile/jgh4529">
    <img src="https://img.shields.io/badge/solved.ac-jgh4529-17CE3A?style=flat-square" alt="solved.ac jgh4529" />
  </a>
  <img src="https://img.shields.io/badge/SSAFY-14th-1A73E8?style=flat-square" alt="SSAFY 14th" />
</p>

---

## 🎯 Focus Areas

- 도메인 경계, public ID, 멱등성, 감사 로그를 고려한 백엔드 API 설계
- WebRTC, MQTT, SSE, Kafka, Redis Pub/Sub, Outbox 기반 실시간 시스템
- Docker Compose, Jenkins, Nginx, Prometheus, Grafana를 활용한 배포/운영 환경 구성
- GPU 추론 서버와 핵심 비즈니스 서버를 분리하는 AI 서비스 연동
- Notion/Jira 기반 요구사항, API 계약, 트러블슈팅, 배포 의사결정 문서화
- 개인 NAS와 홈네트워크 기반 실제 서비스 배포/운영 경험
- BOJ / solved.ac 기반 알고리즘 학습: 그래프 탐색, 백트래킹, 동적 계획법 중심

---

## 📝 Engineering Workflow

- Notion과 Jira를 활용해 요구사항, API 계약, 트러블슈팅, 배포 의사결정, 회고를 기록합니다.
- 문제 발생 시 원인, 해결 과정, 재발 방지 관점으로 정리하고 팀원이 다시 참고할 수 있는 형태로 남기려고 합니다.
- 코드뿐 아니라 운영 방식과 의사결정 근거가 남는 개발을 중요하게 생각합니다.

---

## 🏠 Personal Ops Lab

- 개인 NAS와 홈네트워크를 운영하며 실제 서비스를 배포하고 유지보수합니다.
- 내부망/외부망 접근, reverse proxy, 도메인 연결, TLS, 백업, 접근 제어를 직접 구성하며 운영 경험을 쌓고 있습니다.
- 배포 이후 로그 확인, 서비스 상태 점검, 장애 대응, 데이터 보존까지 고려하는 운영 습관을 만들고 있습니다.

---

## 🚀 Featured Projects

### MoM

> 360도 촬영 기반 3DGS 인체 아바타 생성·체형 측정·AI 피드백 서비스

- 기간: 2026.04.17 - 2026.05.28
- 역할: AI, 3DGS, Body Measurement, Infra, MLOps
- 저장소: GitHub 미공개
- 기술 스택: Python, 3D Gaussian Splatting, SMPL, COLMAP, SPZ, GLB, RabbitMQ, MinIO, Docker, GitLab CI/CD, tmux, Linux
- 주요 기여:
  - 근거 지표: Jira 담당 118건, 보고 110건, 작성·병합 MR 59건, critical path `586.814s -> 336.180s` 42.7% 감소, mask split/dilation `~159.968s -> ~1.9s` 98.8% 감소
  - 360도 촬영 영상 기반 단일 인체 재구성 파이프라인을 구성하고, 3DGS 렌더링 엔진과 신체 측정 엔진을 분리
  - frame extraction, subject mask, masked COLMAP, 3DGS train, postprocess, SPZ/GLB export, measurement export로 이어지는 stage 기반 파이프라인 설계
  - `preprocess`, `fit`, `measure-export` 단계로 SMPL 기반 신체 측정 엔진을 분리하고 `measurement_report.json` 산출 계약 정리
  - RabbitMQ 기반 avatar request/response 흐름과 MinIO artifact 업로드, presigned URL 전달 구조 설계
  - GPU 서버에서 Docker 대신 tmux worker로 장시간 3DGS job을 실행하고 stage timing, run manifest, stdout/stderr log를 남기도록 운영화
  - mask reprojection 기반 sparse filtering, postprocess Gaussian pruning, contour refine, dark artifact cleanup을 적용해 신체 주변 배경/노이즈 point를 제거
  - postprocess 결과를 PLY/SPZ viewer artifact와 연결하고 source geometry, training camera, measurement coordinate는 훼손하지 않도록 export-only 보정 원칙 적용
  - critical path를 `586.814s -> 336.180s`로 줄이고, mask split/dilation 병목을 `~159.968s -> ~1.9s` 수준으로 개선

### Waddoc

> 전화로 예약하면 집 앞까지 찾아오는 방문형 비대면 원격 진료 자율주행 로봇 서비스

- 기간: 2026.03.09 - 2026.04.18
- 역할: 백엔드, MSA 설계, 인프라, 모니터링, AI-IDV 본인확인 서버 구현/연동
- 저장소: [github.com/hwan515/waddoc](https://github.com/hwan515/waddoc)
- 기술 스택: Spring Boot, PostgreSQL, Redis, Kafka, LiveKit, MQTT, Docker Compose, Jenkins, Nginx, Prometheus, Grafana, FastAPI, SCRFD, AdaFace, PaddleOCR, ONNX Runtime
- 주요 기여:
  - 근거 지표: 전체 Jira 432건 중 담당 201건(46.5%), 보고 219건(50.7%), 트러블슈팅/버그 21건, 4-service 구조, MQTT 토픽 7종, Redis Pub/Sub fan-out, Kafka/Outbox
  - 예약, 미션, 진료 세션, 보호자, 관리자, 로봇 관제 도메인을 분리해 MSA 서비스 경계와 통신 흐름 설계
  - 예약, 미션, 진료 세션, 보호자, 관리자, 로봇 운영 흐름을 위한 RESTful API와 도메인 플로우 설계
  - Kafka와 dual Outbox를 활용한 배차/비즈니스 이벤트 처리
  - Redis Pub/Sub fan-out 기반 scale-out SSE 알림 구조 구현
  - 로봇 관제 통신을 MQTT over WSS 구조로 전환하고 telemetry cache, stale payload 방어 로직 적용
  - Jenkins 변경 경로 기반 배포, monitoring stack, Grafana 접근 제어 구성
  - FastAPI 기반 AI-IDV 본인확인 서버를 구현하고 SCRFD 얼굴 검출, AdaFace 얼굴 임베딩 비교, PaddleOCR 신분증 OCR 파이프라인을 구성
  - PaddleOCR 결과 구조화와 OCR 필드 재검증으로 신분증 본인확인 false negative 완화
  - AdaFace checkpoint를 ONNX로 변환하고 FP16/INT8 양자화 및 FP32 대비 임베딩 유사도/latency 비교 스크립트를 정리
  - Spring Boot와 multipart 계약으로 연동하고 OCR/얼굴 대조 결과를 도메인 규칙으로 재검증

### BankBank

> 예금 비교부터 카드 추천까지 다루는 SSAFY 통합 금융 서비스

- 기간: 2025.12
- 역할: 팀장, 백엔드, 추천 시스템, 챗봇
- 저장소: [github.com/hwan515/bankbank](https://github.com/hwan515/bankbank)
- 기술 스택: Django, DRF, Vue, MySQL, ChromaDB, OpenAI API, Redis, WebSocket, Docker, Nginx, Daphne
- 주요 기여:
  - 근거 지표: 카드 데이터 수집 -> MySQL 마이그레이션 -> 혜택 정제 -> ChromaDB 동기화 4단계 파이프라인, 15개 혜택 카테고리, Function Calling 도구 5개
  - 예금/적금 상품 저장, 목록 조회, 상세 조회, 관심 상품 가입/해제 기능 구현
  - Card-Gorilla API 기반 카드 데이터 크롤링, SQLite 저장, MySQL 마이그레이션 파이프라인 구성
  - SQL hard filter와 ChromaDB semantic search를 결합한 하이브리드 카드 추천 시스템 구현
  - 사용자 프로필 기반 추천과 자연어 질의 기반 추천을 분리하고 연회비/전월실적 조건을 후보군 단계에서 제어
  - OpenAI Function Calling 기반 금융 챗봇에서 카드 추천, 상품 검색, 가입 상품 조회 도구 연동
  - WebSocket 채팅, 커뮤니티 게시판, Docker 기반 배포 구성 담당

### Metanet - Final PTJ

> MSA 서비스를 OpenStack 기반 하이브리드 클라우드 환경에 배포하는 인프라 프로젝트

- 기간: 2025.02
- 역할: Kubernetes 클러스터 구축, 네트워크/배포 자동화, CI/CD 인프라 구성
- 자동화 스크립트: [github.com/hwan515/kubernetes-Project/tree/main/k8s](https://github.com/hwan515/kubernetes-Project/tree/main/k8s)
- 기술 스택: OpenStack, Kolla-Ansible, Kubernetes, kubeadm, CRI-O, Flannel, MetalLB, Ingress Nginx, HAProxy, Keepalived, Jenkins, Harbor, Shell, Linux, Terraform, Ansible
- 주요 기여:
  - 근거 지표: Kubernetes 자동화 스크립트 5개, Kubernetes/CRI-O v1.30, Calico v3.27.5, kubeadm init/join, Helm, CNI 설치 자동화
  - OpenStack 기반 VM 환경에서 controller / compute 노드 IP convention을 정의하고 Kubernetes 클러스터 구조 설계
  - `kubeadm`, `CRI-O`, `kubelet`, `kubectl` 설치와 커널 모듈, swap, SELinux, sysctl 설정을 쉘 스크립트로 자동화
  - HAProxy와 Keepalived를 이용해 Kubernetes API Server VIP를 구성하고 멀티 컨트롤러 노드 조인 구조 설계
  - kubeadm init/join, CRI-O, Helm, CNI 설치 스크립트를 분리하여 클러스터 재배포 시간을 단축
  - MetalLB IPAddressPool / L2Advertisement / BGP 설정을 환경별 네트워크 대역에 맞게 조정하고 LoadBalancer 노출 문제 해결
  - Jenkins, Harbor, GitLab 기반 CI/CD 흐름과 Kubernetes 배포 명세를 정리해 MSA 서비스 배포 기반 마련

---

## 🧭 Experience

| 기간 | 과정 | 주요 내용 |
| --- | --- | --- |
| 2025.07 - 2026.06 | SSAFY 14기 | Django/DRF, Vue, Spring Boot, RAG/LLM, ChromaDB, 3DGS, SMPL, RabbitMQ, Kafka, MinIO, Docker, GitLab CI/CD, 실시간 통신, GPU worker/MLOps |
| 2024.12 - 2025.02 | Metanet Cloud Engineer | OpenStack, Kubernetes, Azure, Terraform, Ansible, GitLab, Jenkins, Harbor, Argo CD |
| 2023.08 - 2024.02 | Shinsegae I&C Cloud Engineer | Flask, React, AWS, Docker, Kubernetes, GitHub Actions, CodeDeploy, React Native, Terraform |

---

## 🏆 Awards & Certifications

- SSAFY 최종 프로젝트 우수상
- SSAFY 특화 프로젝트 우수상
- Metanet Cloud Engineer 장려상
- SQLD
- Microsoft Azure Fundamentals AZ-900

---

## 🛠️ Skill Ladder

| Level | Capability | Main Tools / Project Evidence |
| --- | --- | --- |
| 1. Application Builder | 도메인 기능을 API와 화면으로 구현 | Java, Python, Spring Boot, Django/DRF, FastAPI, Vue, React |
| 2. Service Designer | 인증, 예약, 미션, 세션 같은 도메인 경계와 MSA 흐름 설계 | PostgreSQL, MySQL, Redis, REST API, public_id, DTO, error code |
| 3. Realtime Integrator | 실시간 알림, 로봇 telemetry, 이벤트 기반 비동기 처리 구성 | Kafka, RabbitMQ, MQTT, SSE, WebSocket, LiveKit, Outbox / Waddoc, MoM |
| 4. AI Pipeline Engineer | RAG/LLM, OCR/Face IDV, 3DGS/SMPL 파이프라인을 서비스와 연결 | OpenAI API, ChromaDB, SCRFD, AdaFace, PaddleOCR, ONNX Runtime, 3DGS, SMPL, MinIO / BankBank, Waddoc, MoM |
| 5. Platform Operator | 배포, 관측, 클러스터 자동화, GPU 작업 운영까지 연결 | Docker, Kubernetes, CRI-O, Calico, Helm, Jenkins, GitLab CI/CD, Nginx, Prometheus/Grafana, OpenStack, Terraform/Ansible, AWS/Azure, Shell / Metanet |

---

## 🧩 Algorithm

<a href="https://solved.ac/profile/jgh4529">
  <img src="https://mazassumnida.wtf/api/v2/generate_badge?boj=jgh4529" alt="solved.ac profile badge for jgh4529" />
</a>

---

## 🔗 GitHub

- 프로필: [github.com/hwan515](https://github.com/hwan515)
- 대표 저장소: [Waddoc](https://github.com/hwan515/waddoc), [BankBank](https://github.com/hwan515/bankbank), [Kubernetes 자동화](https://github.com/hwan515/kubernetes-Project/tree/main/k8s)
- 프로젝트 노트, 트러블슈팅 기록, API 계약, 배포 의사결정을 코드와 함께 관리하려고 합니다.
