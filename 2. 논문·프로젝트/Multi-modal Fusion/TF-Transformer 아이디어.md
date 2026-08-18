프로젝트: [[Multi-modal Fusion]]

[[Multi-modal Time Series Analysis A Tutorial and Survey]]
FT-Transformer로 메타데이터 인코딩 후 cross-attention 적용 시, 시계열을 query로 두는 게 이 논문의 표준 패턴과 일치



- **Fusion**: 여러 모달리티의 표현(또는 출력)을 결합해 상호 보완적 정보를 통합하는 것 (addition/concatenation 등)
- **Alignment**: 서로 다른 모달리티 간의 관계를 시간적·의미적으로 일치시켜 정합성을 확보하는 것 (self/cross-attention, gating 등)
- **Transference**: 한 모달리티의 정보를 다른 모달리티로 변환·생성·전이시키는 것 (예: 시계열→텍스트, 이미지→임베딩)