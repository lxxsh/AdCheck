# 🔍 AdCheck — 허위·과장 광고 의심도 분석 서비스

> 기능성 화장품 광고 문구와 이미지를 입력하면 AI가 허위·과장 가능성을 분석하고  
> 의심도 점수(0.0~1.0)와 이유를 제공하는 웹 서비스입니다.

<br>

## 🔗 레포지토리

| 파트 | 링크 |
|------|------|
| AI 분석 서버 | [AdCheck_analysis](https://github.com/Jun0913/AdCheck_analysis) |
| 백엔드 | [AdCheck_backend](https://github.com/Jun0913/AdCheck_backend) |
| 프론트엔드 | [Adcheck_frontend](https://github.com/lxxsh/Adcheck_frontend) |

<br>

## 📌 프로젝트 개요

| 항목 | 내용 |
|------|------|
| 분류 | 졸업 프로젝트 (4인 팀) |
| 기간 | 2025 |
| 담당 | 데이터 수집·라벨링 / 프론트엔드 UI·UX 설계 |
| 대상 도메인 | 기능성 화장품 광고 |

<br>

## 🎯 프로젝트 목표

소비자가 광고 문구나 이미지를 입력하면 허위·과장 가능성을 자동으로 판별하고,  
**왜 의심스러운지 이유까지 함께 제공**해 소비자 스스로 광고를 비판적으로 판단할 수 있도록 돕는 서비스입니다.

<br>

## 👤 내 역할

### 1. 데이터 수집 및 라벨링

기능성 화장품 광고 판별 모델 학습을 위한 **데이터셋을 처음부터 직접 구축**했습니다.

**수집 과정**
- 올리브영, 메디큐브 등 주요 뷰티 쇼핑몰 광고 페이지에서 광고 문구 수작업 크롤링
- 팀 전체 수집량: 약 7,000~8,000건 / 개인 담당: 약 2,000건

**라벨링 기준**
- 식품의약품안전처(식약처) 및 공공기관의 기능성 화장품 관련 규정을 직접 조사
- 금지 표현 / 허용 표현 / 의심 표현 3단계 기준을 팀원들과 함께 정의
- 라벨: 금지=0 / 허용=1 / 의심도: 주의·의심·정상

> 단순 수집이 아닌 **도메인 규정을 공부하고 라벨 기준을 직접 설계**한 경험으로,  
> 데이터 품질이 모델 성능의 핵심임을 직접 체감했습니다.

---

### 2. 프론트엔드 UI·UX 설계

바이브코딩 방식으로 프론트엔드 전체를 처음부터 끝까지 담당했습니다.

- 전체 사이트 디자인 및 레이아웃 설계
- 각 요소의 크기·배치·색상 등 시각적 구성 결정
- **"사용자가 광고 문구를 입력하고 결과를 직관적으로 이해할 수 있는가"** 를 중심으로 UX 고민
- 의심도 점수와 이유 설명을 사용자 친화적으로 표시하는 결과 화면 설계

<br>

## 🏗 시스템 아키텍처

```
[React 프론트엔드]
        ↓
[Spring Boot 백엔드]
        ↓
[FastAPI AI 분석 서버]
        ↓
[Google Vision OCR] → [전단 필터] → [규칙 기반 엔진] → [KoBERT]
        ↓
  의심도 점수 + 이유 반환
```

- DB: MySQL / PostgreSQL
- OCR fallback: EasyOCR, PaddleOCR
- 배포: Docker

<br>

## 🤖 AI 분석 파이프라인 (팀원 담당)

| 단계 | 설명 |
|------|------|
| 0차 — 전단 필터 | 광고·화장품 도메인 무관 문장 사전 제거 (scikit-learn) |
| 1차 — 규칙 기반 엔진 | 화이트리스트·금지 키워드·패턴 태그 기반 의심도 판정 |
| 2차 — KoBERT | 문장 전체 문맥 분석, 연속 의심도 점수(0.0~1.0) 산출 |

> AI 파이프라인은 팀원이 담당했으며, 본인은 해당 모델이 학습할 수 있도록  
> **데이터 기반(수집·라벨링)을 구축**하는 역할을 맡았습니다.

<br>

## 🛠 기술 스택

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![React](https://img.shields.io/badge/React-61DAFB?style=flat-square&logo=react&logoColor=black)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-6DB33F?style=flat-square&logo=springboot&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=flat-square&logo=mysql&logoColor=white)

<br>

## 💡 배운 점

- **데이터가 모델을 만든다** — 라벨 기준을 어떻게 설계하느냐에 따라 모델 성능이 완전히 달라진다는 걸 직접 경험했습니다.
- **도메인 지식의 중요성** — 식약처 규정을 공부하지 않았다면 정확한 라벨링이 불가능했을 것입니다.
- **사용자 관점의 설계** — 분석 결과를 단순히 점수로만 보여주는 것이 아니라, 사용자가 이해할 수 있는 형태로 전달하는 것이 중요하다는 걸 UI 설계를 통해 배웠습니다.

<br>

---

> 📬 **이석하** · [GitHub](https://github.com/lxxsh)
