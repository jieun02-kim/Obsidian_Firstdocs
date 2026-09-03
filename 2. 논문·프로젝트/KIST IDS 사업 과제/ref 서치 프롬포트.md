



### 프롬포트
모듈형 로봇(modular robot)의 "실시간 재구성(real-time reconfiguration)"과 
"재구성 방법론(reconfiguration methodology)"을 다루는 선행연구를 조사해줘.

[범위]
- 멀티모달 센서 융합, 딥러닝 기반 인식, 그래프이론 기반 토폴로지 표현
  (그래프 동형사상, 그래프 스펙트럼 매칭 등)은 제외해줘.
- 대신 다음에 집중해줘:
  (1) 초기 구성에서 목표 구성으로 실제로 바꾸는 재구성 계획/제어 
      알고리즘 (순차적/병렬/분산 방식 모두 포함)
  (2) 재구성 속도, 동작 원시(motion primitive), 실시간성을 확보하기 
      위한 방법론 (예: 병렬 재구성, 경량 동작 시퀀싱, 온라인 재계획)
  (3) 재구성을 지원하는 기구 설계 (커넥터, 액추에이터, 최소 자유도 
      설계 등 하드웨어 접근)
  (4) 재구성 도중/직후 제어기를 즉시 재사용 가능하게 만드는 방법론

[이미 알고 있는 레퍼런스 — 중복 제외]
- Liu, Whitzer, Yim, "A Distributed Reconfiguration Planning Algorithm 
  for Modular Robots," RAL 2019
- Gerbl & Gerstmayr, "Self-Reconfiguration of PARTS: A Parallel 
  Reconfiguration Algorithm Based on Surface Flow," RAS 2023
- Gerbl, Pieber, Ulrich, Gerstmayr, "PARTS," Robotics 2024
- Gu et al., "MODUR: A Modular Dual-reconfigurable Robot," IROS 2025
- RhoMorph (arXiv 2026) — morphpivoting 동작 원시
- Romiti et al., "Toward a Plug-and-Work Reconfigurable Cobot," 
  IEEE/ASME T-Mech 2021/2022
- Tu, Liang, Wu, Li, Lam, "Locomotion and self-reconfiguration 
  autonomy for spherical freeform modular robots," IJRR 2025

[원하는 것]
- 위 목록과 중복되지 않는, 특히 2023~2026년 최신 논문 위주로 찾아줘
- 저자, 연도, 학회/저널, 한두 문장 요약, 그리고 "왜 실시간/방법론 
  측면에서 의미 있는지"를 함께 제시해줘
- IEEE Xplore, Science Robotics, IJRR, RAS, arXiv cs.RO를 우선 훑어줘
- Mark Yim(UPenn ModLab), Tin Lun Lam(CUHK-Shenzhen), 
  Johannes Gerstmayr(Innsbruck), Jamie Paik(EPFL) 그룹의 
  최신 후속연구도 확인해줘