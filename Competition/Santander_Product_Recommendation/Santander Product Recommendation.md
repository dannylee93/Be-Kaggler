## Santander Product Recommendation

> 산탄데르 제품 추천 데이터 분석대회 관련 정리 파일

<p align='center'><img src='https://storage.googleapis.com/kaggle-competitions/kaggle/5558/logos/front_page.png' alt="img" style="zoom:67%;" /></p>

### Description

현재 산탄데르 은행은 소수의 고객에게만 다양한 제품 추천이 제공되고, 나머지 고객에게는 기회가 적어 고객 경험이 불균등한 상황이다. 이 대회에서, 고객의 과거이력과 유사한 고객군들의 데이터를 기반으로 다음 달 해당 고객이 무슨 제품을 사용할 지 예측하는 문제를 준비했다. 효과적인 시스템을 갖추어 고객이 인생의 어느 단계에 있든 고객에 필요에 맞는 제품을 추천할 것이다.

매일 은행을 방문하는 몇 만명의 고객에게 1:1 맞춤 금융 제품을 추천하기 위해 머신러닝 알고리즘을 활용하기로 결정하였고, 고객의 나이,연봉,결혼 유무, 거주 지역 등의 정보를 토대로 이상적인 제품을 추천하려는 이유에서 출발했다.

### Evaluation

고객이 신규로 구매할 제품이 무엇인지 예측하는 대회이다. 여기서 '신규 구매 제품' 이란 지난 달 기준으로 고객이 보유하고 있지 않은 금융 제품 중, 이번 달에 신규로 구매하게 된 제품 이다.

즉, 지난 달 보유하지 않은 금융 제품 중 이번달 구매할 것으로 예측되는 상위 7개 이다.

평가 척도로 사용되는 `MAP@7`은 Mean Average Precision@7 이란 의미로 예측 정확도의 평균을 의미하며 `@7`은 최대 7개 까지 라는 의미 이다.

## EDA(Exploratory Data Analysis)

> 산탄데르 제품 추천 경진대회는 Tabular 형태의 시계열 데이터를 제공한다.

주어진 데이터를 가지고 그대로 사용하는 것이 아니라, 데이터 노이즈가 그대로 반영되어 있기 때문에 결측치, 이상치 등 다양한 노이즈를 탐색하며 분석해야한다.

| 변수 명               | 설명                                                         |
| :-------------------- | :----------------------------------------------------------- |
| fecha_dato            | 날짜                                                         |
| ncodpers              | 고객 고유식별번호                                            |
| ind_empleado          | 고용지표 : A active, B ex employed, F filial, N not employee, P pasive |
| pais_residencia       | 고객의 거주 국가                                             |
| sexo                  | 성별                                                         |
| age                   | 나이                                                         |
| fecha_alta            | 고객의 첫 계약 날짜                                          |
| ind_nuevo             | 신규 고객 지표. (6개월 이내 신규 고객일 경우, ==1)           |
| antiguedad            | 은행 거래 누적 기간(월)                                      |
| indrel                | 고객 등급(1: 1등급 고객, 99: 해당 달에 고객 1등급이 해제되는 1등급 고객) |
| ult_fec_cli_1t        | 1등급 고객으로서의 마지막 날짜 (월말이 아닌 경우)            |
| indrel_1mes           | 월초 기준 고객 등급, 1 (First/Primary customer), 2 (co-owner ),P (Potential),3 (former primary), 4(former co-owner) |
| tiprel_1mes           | 월초 기준 고객 관계 유형, A (active), I (inactive), P (former customer),R (Potential) |
| indresi               | 거주 지표(고객의 거주 국가와 은행이 위치한 국가 동일 여부), S(맞음)/N(아님) |
| indext                | 외국인 지표(고객의 태어난 국가와 은행이 위치한 국가 동일한지 여부), S(맞음)/N(아님) |
| Conyuemp              | 배우자 지수(고객이 직원의 배우자 인 경우 1)                  |
| canal_entrada         | 고객 유입 채널                                               |
| indfall               | 고객의 사망 여부. N / S                                      |
| tipodom               | 주소 유형. (1, 기본 주소)                                    |
| cod_prov              | 지방 코드(주소 기반)                                         |
| nomporv               | 지방 이름                                                    |
| ind_actividad_cliente | 활발성 지표(1, active customer; 0, inactive customer)        |
| renta                 | 가구의 총수입                                                |
| 세그먼트              | 분류(01-VIP, 02-개인, 03-대졸)                               |
| ind_ahor_fin_ult1     | 예금                                                         |
| ind_aval_fin_ult1     | 보증                                                         |
| ind_cco_fin_ult1      | 당좌 예금                                                    |
| ind_cder_fin_ult1     | 파생 상품 계좌                                               |
| ind_cno_fin_ult1      | 급여 계정                                                    |
| ind_ctju_fin_ult1     | 주니어(청소년) 계정                                          |
| ind_ctma_fin_ult1     | 마스 특별 계정                                               |
| ind_ctop_fin_ult1     | 특정 계정                                                    |
| ind_ctpp_fin_ult1     | 특정 플러스 계정                                             |
| ind_deco_fin_ult1     | 단기 예금                                                    |
| ind_deme_fin_ult1     | 중기 예금                                                    |
| ind_dela_fin_ult1     | 장기 예금                                                    |
| ind_ecue_fin_ult1     | e - 계정                                                     |
| ind_fond_fin_ult1     | 펀드                                                         |
| ind_hip_fin_ult1      | 부동산 대출                                                  |
| ind_plan_fin_ult1     | 연금                                                         |
| ind_pres_fin_ult1     | 대출                                                         |
| ind_reca_fin_ult1     | 세금                                                         |
| ind_tjcr_fin_ult1     | 신용 카드                                                    |
| ind_valo_fin_ult1     | 증권                                                         |
| ind_viv_fin_ult1      | 홈 계정                                                      |
| ind_nomina_ult1       | 급여                                                         |
| ind_nom_pens_ult1     | 연금                                                         |
| ind_recibo_ult1       | 직불 카드                                                    |



