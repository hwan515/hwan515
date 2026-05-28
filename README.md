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
- BOJ / solved.ac 기반 알고리즘 학습: 그래프 탐색, 백트래킹, 동적 계획법 중심

---

## 🚀 Featured Projects

### MoM

> 360도 촬영 기반 3DGS 인체 아바타 생성·체형 측정·AI 피드백 서비스

- 기간: 2026.04.17 - 2026.05.28
- 역할: AI, 3DGS, Body Measurement, Infra, MLOps
- 저장소: GitHub 미공개
- 기술 스택: Python, 3D Gaussian Splatting, SMPL, COLMAP, SPZ, GLB, RabbitMQ, MinIO, Docker, GitLab CI/CD, tmux, Linux
- 주요 기여:
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
- 역할: 백엔드, MSA 설계, 인프라, 모니터링, AI 연동
- 저장소: [github.com/hwan515/waddoc](https://github.com/hwan515/waddoc)
- 기술 스택: Spring Boot, PostgreSQL, Redis, Kafka, LiveKit, MQTT, Docker Compose, Jenkins, Nginx, Prometheus, Grafana, FastAPI
- 주요 기여:
  - 예약, 미션, 진료 세션, 보호자, 관리자, 로봇 관제 도메인을 분리해 MSA 서비스 경계와 통신 흐름 설계
  - 예약, 미션, 진료 세션, 보호자, 관리자, 로봇 운영 흐름을 위한 RESTful API와 도메인 플로우 설계
  - Kafka와 dual Outbox를 활용한 배차/비즈니스 이벤트 처리
  - Redis Pub/Sub fan-out 기반 scale-out SSE 알림 구조 구현
  - 로봇 관제 통신을 MQTT over WSS 구조로 전환하고 telemetry cache, stale payload 방어 로직 적용
  - Jenkins 변경 경로 기반 배포, monitoring stack, Grafana 접근 제어 구성
  - 외부 GPU 서버의 FastAPI 본인확인 추론 서비스와 Spring Boot 도메인 규칙 연동

### BankBank

> 예금 비교부터 카드 추천까지 다루는 SSAFY 통합 금융 서비스

- 기간: 2025.12
- 역할: 팀장, 백엔드, 추천 시스템, 챗봇
- 저장소: [github.com/hwan515/bankbank](https://github.com/hwan515/bankbank)
- 기술 스택: Django, DRF, Vue, MySQL, ChromaDB, OpenAI API, Redis, WebSocket, Docker, Nginx, Daphne
- 주요 기여:
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
| 2025.07 - 현재 | SSAFY 14기 | Django/DRF, Vue, Spring Boot, RAG/LLM, ChromaDB, 3DGS, SMPL, RabbitMQ, Kafka, MinIO, Docker, GitLab CI/CD, 실시간 통신, GPU worker/MLOps |
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

## 🛠️ Tech Stack

### 1. Service Backend

도메인 모델링, REST API, 인증/인가, MSA 서비스 경계 설계, 외부 AI API 연동을 담당합니다.

![Java](https://img.shields.io/badge/Java-007396?style=flat-square&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-6DB33F?style=flat-square&logo=springboot&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![Django](https://img.shields.io/badge/Django-092E20?style=flat-square&logo=django&logoColor=white)
![DRF](https://img.shields.io/badge/DRF-A30000?style=flat-square&logo=django&logoColor=white)
![Flask](https://img.shields.io/badge/Flask-000000?style=flat-square&logo=flask&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)

### 2. Client Experience

사용자 화면, 관리자 화면, 실시간 상태 표시, API 연동 UI를 구현합니다.

![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)
![React](https://img.shields.io/badge/React-61DAFB?style=flat-square&logo=react&logoColor=black)
![Vue.js](https://img.shields.io/badge/Vue.js-4FC08D?style=flat-square&logo=vuedotjs&logoColor=white)

### 3. AI & Data Pipeline

RAG/LLM, 3DGS, 신체 측정 파이프라인, 벡터 검색, 객체 저장소 기반 artifact 흐름을 설계합니다.

![OpenAI](https://img.shields.io/badge/OpenAI_API-412991?style=flat-square&logo=openai&logoColor=white)
![ChromaDB](https://img.shields.io/badge/ChromaDB-5F4B8B?style=flat-square&logo=databricks&logoColor=white)
![3DGS](https://img.shields.io/badge/3DGS-111827?style=flat-square&logo=threedotjs&logoColor=white)
![SMPL](https://img.shields.io/badge/SMPL-374151?style=flat-square&logo=python&logoColor=white)
![COLMAP](https://img.shields.io/badge/COLMAP-2563EB?style=flat-square&logo=opencv&logoColor=white)
![MinIO](https://img.shields.io/badge/MinIO-C72E49?style=flat-square&logo=minio&logoColor=white)

### 4. Realtime & Event Flow

실시간 알림, 로봇 telemetry, 이벤트 기반 처리, 메시지 브로커 기반 비동기 흐름을 구성합니다.

![Kafka](https://img.shields.io/badge/Kafka-231F20?style=flat-square&logo=apachekafka&logoColor=white)
![RabbitMQ](https://img.shields.io/badge/RabbitMQ-FF6600?style=flat-square&logo=rabbitmq&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-FF4438?style=flat-square&logo=redis&logoColor=white)
![WebSocket](https://img.shields.io/badge/WebSocket-010101?style=flat-square&logo=socketdotio&logoColor=white)
![MQTT](https://img.shields.io/badge/MQTT-660066?style=flat-square&logo=mqtt&logoColor=white)
![LiveKit](https://img.shields.io/badge/LiveKit-111827?style=flat-square&logo=webrtc&logoColor=white)

### 5. Infra & Operations

컨테이너 배포, Kubernetes 클러스터 구축, CI/CD, 모니터링, IaC, 클라우드 운영을 다룹니다.

![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=flat-square&logo=mysql&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-FF4438?style=flat-square&logo=redis&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat-square&logo=linux&logoColor=black)
![Shell](https://img.shields.io/badge/Shell-4EAA25?style=flat-square&logo=gnubash&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=flat-square&logo=kubernetes&logoColor=white)
![OpenStack](https://img.shields.io/badge/OpenStack-ED1944?style=flat-square&logo=openstack&logoColor=white)
![GitLab CI/CD](https://img.shields.io/badge/GitLab_CI/CD-FC6D26?style=flat-square&logo=gitlab&logoColor=white)
![Jenkins](https://img.shields.io/badge/Jenkins-D24939?style=flat-square&logo=jenkins&logoColor=white)
![Harbor](https://img.shields.io/badge/Harbor-60B932?style=flat-square&logo=harbor&logoColor=white)
![Nginx](https://img.shields.io/badge/Nginx-009639?style=flat-square&logo=nginx&logoColor=white)
![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?style=flat-square&logo=prometheus&logoColor=white)
![Grafana](https://img.shields.io/badge/Grafana-F46800?style=flat-square&logo=grafana&logoColor=white)
![Terraform](https://img.shields.io/badge/Terraform-844FBA?style=flat-square&logo=terraform&logoColor=white)
![Ansible](https://img.shields.io/badge/Ansible-EE0000?style=flat-square&logo=ansible&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-232F3E?style=flat-square&logo=amazonwebservices&logoColor=white)
![Azure](https://img.shields.io/badge/Azure-0078D4?style=flat-square&logo=microsoftazure&logoColor=white)

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
