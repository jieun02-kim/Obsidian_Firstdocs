

- [ ] 메타데이터 구체화
- [ ] [MetaData - Topology/Module/State Info - 각 축의 cfg file] 구조 수립을 위한 각 데이터 항목 도출
- [ ] 제어 가능 상태 진입을 위한 상태운용 절차별 단계 구현
- [ ] ref 스터디하며 fusion 구체적 방법론 구상



## 시계열 논문 서베이 다음 ref

- TaTS[49] Input Stage Fusion  
    굳이 시계열 모델의 구조를 바꿀 필요 없이, 텍스트 정보를 수치 시계열과 똑같은 형태(차원)로 변환  
    -> 실시간 시계열에 적용 가능한지?  
    -> input-level fusion인데, 보통 시계열 -> 숫자로 변환해서 llm에 통째로 넣거나 복잡한 크로스 어텐션 사용하지만 이 논문은 input fusion의 한계를 보완한건지

- MOAT [42] Output Stage Fusion  
    멀티모달 시계열 예측을 위한 2단계 프레임워크를 도입  
    1단계에서는 분해된 시계열과 텍스트 임베딩으로부터 예측을 생성하도록 모델을 최적화  
    2단계에서는 MLP를 통한 오프라인 종합(synthesis)을 적용하여 서로 다른 구성 요소들을 동적으로 융합

## 내용 중 가져갈 개념

- input-level Transference 방법 서치  
    규칙 기반 변환이므로 초기 metadata->활용가능 모달리티 원형으로 변경하기 위한 변환 규칙으로 사용 (관련 ref에 뭐가 있는지 알아보기)
- Tabular Transform ref로 할지 input에서 전이할지 보기
- claude에 검색한 기본 코드 분석  
