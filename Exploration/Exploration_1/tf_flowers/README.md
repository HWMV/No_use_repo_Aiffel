# Exploration 01 Report
# Flower_Test_Final 파일만 보시면 됩니다!
# review file은 따로 만들었습니다.

### Test 06까지 다양한 하이퍼 파라미터 조절 시 성능 변화 입니다

---
### 온라인 코어 6기 최현우

flower image classification
pre-trained model : ResNet50 , 50v2
Data Augmentation 공통 적용
BATCH_SIZE = 4 공통 적용

---
# 1. Test 01

* Epoch : 80
* lr = 0.001
* Loss: 1.13 , ACC: 0.5625

과적합 되진 않았으나, acc가 일정 성능에서 증가하지 않고 수렴

# 2. Test 02

* Epoch : 30
* lr = 0.0001
* lrScheduler : 5 epochs 마다 반감
* ealryStopping : patience=6
* Loss: 1.42 , ACC: 0.5000

# 3. Test 03

* fine_Tune : 하위 10개 레이어 학습 (저소자 추출)
* lr = 0.0001
* 스케쥴러 동일
* epochs = 30
* Loss: 0.35 , ACC: 0.8875

# 4. Test 04
저장할 때 잘못해서 덮어 씌어짐 ㅠㅠ..

# 5. Test 05

* ResNetV2로 모델 변경
* 위와 동일 Data 증강만 삭제
* Loss: 0.74 , ACC: 0.8250
  
# 6. Test 06

* 위와 동일 Data 증강 넣고 Dense unit 32 > 1000 증가
* 성능 저하 : Acc : 91.25% > 76%

# Test Final

* LrS 지수함수 변경 (0.0001 부근에서 성능이 좋아 그 부분에서 점점 감소하게 설정)
* Fine Tune 상위 레이어 20개(Domain feature 추출)
* 데이터셋 비율 변경

# 전체 수정 과정

1. acc, loss가 일정치를 못 넘고 수렴 (과적합은 X)
2. 학습을 더 잘 진행할 수 있도록 lr 조절
3. 내 데이터에서 저소자 수준의 데이터 추출하기 위해 Fine_Tune
4. model ResNet50 > ResNet50V2 변경 (같은 조건일 때 영향이 가장 큼) 25% 차이
5. Data 증강 (유무로 데이터 영향도 큼 확인) 15% 차이
6. validation 학습을 위해 데이터 비율 조절 (65:15:20)
7. Domain feature 추출 위해 Fine Tune, Lrs 000.1 부근에서 validation 및 train 학습 잘됨을 확인. 스케쥴러로 0.0001 인근에서 점차 감소하게 지수 함수 설정

# pre-trained model 영향 순위
  1. 적절한 모델을 사용하기
  2. 데이터의 양과 질
  3. Fine_Tune
  4. LrS 조절
  5. earlystopping, epoch 조절
  6. earlystopping, epoch 조절
