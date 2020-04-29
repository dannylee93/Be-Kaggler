# Brief Competition

> Kaggle competition 에서 본격적으로 데이터 분석을 하기 전, 어떤 대회와 데이터 인지 천천히 읽고 알아본 다음, 다른 사람들이 해 놓은 커널도 천천히 살피면서 시야를 넓히자.



![](https://scontent-ssn1-1.xx.fbcdn.net/v/t31.0-8/22048009_10155798238193464_5349169435161795951_o.png?_nc_cat=107&_nc_sid=da1649&_nc_oc=AQmhepnq1xjugXGR_b3YyLLD_TdhUxvh6EOF7jGpHozLR1_SoztwLoeSpdUzXm2t3Ig&_nc_ht=scontent-ssn1-1.xx&oh=f1c1c6ee23723c36c3bfdfdd85d001bf&oe=5EB8E8B9)



## OverView

> 데이터 분석 대회의 간략한 소개와 방식들에 대한 정리가 되어있다.



#### Description

보험 청구서가 나오기도 전에 차를 바꿔야 되면 그것만큼 아픈게 없다. 만약 운전을 잘하고 조심하는 사람이라면, 보험료를 보다 많이 내는 것은 공평하지 않아보인다.

브라질의 최대 자동차 및 주택 소유 보험 회사 중 하나인 Porto Seguro는 이런 이슈에 공감하며,대회를 만들었다.

보험금 청구를 할 때 예측이 부정확하면, 잘하고 있는 운전자 한테 보험금을 많이 청구하게 되고 나쁜 운전자에게는 덜 청구하게 된다.

이 대회에서는 **자동차 보험 청구에 대한 예측 모델**을 만든다.



#### Evaluation

1. Scoring Metric
   - 제출된 파일은 정규화된 지니 계수를 사용하여 평가된다.
   - 점수를 매기는 동안, 관측치는 가장 큰 예측부터 가장 작은 예측까지 정렬된다.
   - 지니 계수의 **범위**는 랜덤 추측의 경우 약 `0`에서 완벽한 점수의 경우 약 `0.5`이다. 이산 계산의 이론상 최대 값은 `(1 - frac_pos) / 2`이다.
   - 정규화된 지니 계수의 이론적 최대값은 `1`이다.

2. 제출파일

   | id     | target |
   | ------ | ------ |
   | 0      | 0.0364 |
   | 1      | 0.0364 |
   | 2      | 0.0364 |
   | 3      | 0.0364 |
   | 4      | 0.0364 |
   | 5      | 0.0364 |
   | 6      | 0.0364 |
   | ...    | ...    |
   | 892816 | 0.0364 |

   > 파일은 헤더를 포함하고 위와같은 형식으로, `target` 은 보험 청구 가능성 예측에 대한 점수다.



## Data Description

> 이 대회는 통해 차량보험 가입자가 청구할 가능성을 예측하는 대회다.



- `train.csv`와 `test.csv` 에서, train 데이터에서는 각각의 사람을 구별하는 **id 숫자**와 **0과1로된 target** 열이 기본적으로 있고 <`ind`, `reg`, `car`, `calc`> 과 같이 비슷한 특징들로 그룹되어 있다.

  ```shell
  #Columns
  id
  target
  ps_ind_01
  ps_ind_02_cat
  ps_ind_03
  ps_ind_04_cat
  ps_ind_05_cat
  ps_ind_06_bin
  ps_ind_07_bin
  ps_ind_08_bin
  ps_ind_09_bin
  ps_ind_10_bin
  ps_ind_11_bin
  ps_ind_12_bin
  ps_ind_13_bin
  ps_ind_14
  ps_ind_15
  ps_ind_16_bin
  ps_ind_17_bin
  ps_ind_18_bin
  ps_reg_01
  ps_reg_02
  ps_reg_03
  ps_car_01_cat
  ps_car_02_cat
  ps_car_03_cat
  ps_car_04_cat
  ps_car_05_cat
  ps_car_06_cat
  ps_car_07_cat
  ps_car_08_cat
  ps_car_09_cat
  ps_car_10_cat
  ps_car_11_cat
  ps_car_11
  ps_car_12
  ps_car_13
  ps_car_14
  ps_car_15
  ps_calc_01
  ps_calc_02
  ps_calc_03
  ps_calc_04
  ps_calc_05
  ps_calc_06
  ps_calc_07
  ps_calc_08
  ps_calc_09
  ps_calc_10
  ps_calc_11
  ps_calc_12
  ps_calc_13
  ps_calc_14
  ps_calc_15_bin
  ps_calc_16_bin
  ps_calc_17_bin
  ps_calc_18_bin
  ps_calc_19_bin
  ps_calc_20_bin
  ```

- 열 이름 중, `bin`은 이진 분류를 나타내고, `cat`은 범주 기능을 나타내는 단어다.

- 이러한 명칭이 없는 열들은 연속적(continuous)이거나 서수적(ordinal)이다.

- `-1`은 안에 값이 없다는 뜻이다.

- `target`은 차량보험 가입자의 보험청구 소송 여부이다.



