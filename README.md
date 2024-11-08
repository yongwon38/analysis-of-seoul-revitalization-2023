# **서울시 구별 활동지수 산출을 통한 지역 활성화 방안 제언**

### **2023 데이터안심구역 활용 공동 경진대회 최우수상 수상**

- 구성 : 팀 프로젝트 (5인)
- 기간 : 2023.10. ~ 2023.11.
- 사용 언어 및 도구 : `Python`(`Jupyter Notebook`), `R`
- 실험 설계 및 검증
    - 도시의 활성화 정도를 파악하기 위한 4개의 분야 산출 
      → 인구지수, 경제·전력지수, 문화지수, 생활지수
    - 각 지수 분야 별 유의 변수 파악(요인분석) 및 지수 산출식 구성(주성분분석)
    - 지수 산출식의 범위를 동일하게 조정(Min-Max Scaling)한 후,  4개의 지수 분야를 종합하여 최종 활성화 지수 산출
        - 설명변수 : 주거환경·상권 측정 변수, 민원·생활 관련 변수, 소비·전력 관련 변수
        - 반응변수 : 산출한 최종 활성화 지수
- 모델 설계
    - 클러스터링
        - K-Means 클러스터링 : 공통된 특성을 보이는 지역구끼리 군집화
          - 설명변수 : 인구지수, 경제·전력지수, 문화지수, 생활지수
          - Elbow Method를 통해 5개의 군집으로 구성
        - 군집 1 - 동부권 : 상대적으로 낮은 경제, 문화 지수
        - 군집 2 - 경제 특화권 : 경제 활동 중심의 광역 경제 생활권
        - 군집 3 - 서부권 : 생활, 경제, 문화 전반에서 균형적인 모습을 보임
        - 군집 4 - 거주 특화권 : 주요 거주 단지, 상대적으로 낮은 경제, 문화 지수
        - 군집 5 - 도심권 : 역사·문화 중심의 도심권, 인구, 생활 지수에서의 개선 필요
    - 감성분석
        - 서울시 내 자치구 별 주민들의 지역 만족도를 정량화하기 위해 민원 데이터에 대한 감성분석 실시
        - 극성 탐지(Polarity Detection) 기법 사용
            - 텍스트 내의 단어의 긍·부정을 탐지해 정량화하여 통계적 기법을 적용해 단어가 나타내는 점수의 총합 및 평균을 계산
            - 부정적인 논조를 띠는 민원 데이터 특성 상, 긍·부정의 분류 모델이 아닌 텍스트 자체가 지닌 부정적 어감의 강도 자체를 계산
            - KNU 한국어 감성사전을 사용해 단어 별 부정점수 계산
    - 공간가중회귀
        - 공간적 변이를 고려한 지리가중회귀(GWR) 모델을 이용
        - LASSO 정규화를 통해 설명변수 중 12개의 변수 선정
        - 대역폭에 따라 지리적 가중치가 변화하는 모델의 특성 상, Cross-Validation을 통해 최적의 대역폭 선정 (대역폭 : 10)
- 결과
    - 모델 성능 및 해석
        - 선형 모델(OLS)의 $R^2$:0.889, 지리가중회귀 모델(GWR)의 $R^2$:0.918
        - 지역 전반적으로 사업체수, 공동주택단지수, 민원 점수, 사회환경, 여성카드소비비율 등이 최종 활성화 지수에 유의하게 높은 영향력을 행사하는 변수로 도출된 것을 확인.
        
- 의의 및 기대효과
    - 지역 별 활성화를 위한 맞춤 방안 도출 가능
        - 생활 관련 지수가 낮게 나타난 종로구는 공공주택단지의 추가 설립이 최종 지수에 긍정적인 영향을 미칠 것으로 예상
        - 부정 민원 점수가 높은 중랑구는, 민원에 대한 응대력을 향상시킨다면 최종 지수에 긍정적인 영향을 미칠 것으로 예상
    - 쇠퇴된 지역을 판단하기 위한 객관적인 지표 산출 → 지방 재정 투자 심사 및 정책 수립 시 활용 가능
    - 서울시 도시 경쟁력 강화 및 지역균형발전 정책 실현
    - 지수를 통해 서울시 내 경제적 기회와 도시 서비스에 대한 보편적 접근성 제공
