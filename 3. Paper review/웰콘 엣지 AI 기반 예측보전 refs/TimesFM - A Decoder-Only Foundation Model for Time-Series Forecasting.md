---
type: literature
source: "Abhimanyu Das, Weihao Kong, Andrew Leach, Shreshth Malkhowia, Rajat Sen 외. TimesFM: A Decoder-Only Foundation Model for Time-Series Forecasting. In Proceedings of the 41st International Conference on Machine Learning (ICML 2024), 2024."
author: "Abhimanyu Das, Weihao Kong, Andrew Leach, Shreshth Malkhowia, Rajat Sen 외 (Google Research)"
year: 2024
venue: "ICML 2024 (International Conference on Machine Learning)"
impact_factor: "N/A (학회논문)"
tags: [time-series, forecasting, foundation-model, zero-shot, transformer, decoder-only]
project: "[[웰콘 엣지 AI 기반 예측보전]]"
created: 2026-08-19
updated: 2026-08-19
---

https://honbul.tistory.com/174


모터드라이버의 실시간 수치 데이터(전류, 온도, 통신 에러 등)를 TimesFM에 입력하여 미래 패턴을 예측
이를 실제 측정값과 비교함으로써 **과열, 부하 누적, 장비 노후화 등 고장 전 이상 징후를 선제적으로 감지하는 예지보전(PdM)의 핵심 예측 엔진**으로 직접 활용 가능할듯


## 핵심 요약
- 별도 재학습 없이 미래 수치를 예측하는 제로샷 시계열 예측(Zero-shot Time-Series Forecasting) 파운데이션 모델 TimesFM 제안
- 아키텍처: Decoder-only Transformer + patching 메커니즘
- 모델 규모: 약 200M(2억) 파라미터
- 학습 데이터: 실세상 및 합성 시계열 데이터 수천억 포인트
- 공개 시점: 2023년 10월 arXiv 최초 공개, 2024년 7월 ICML 학회 발표
- 공식 코드: GitHub(google-research/timesfm), Hugging Face 공개




## 메모
- 사용자 제공 정보 기반 1차 등록. 상세 리뷰는 추후 진행.
