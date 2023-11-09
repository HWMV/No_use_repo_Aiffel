# MQ4. PNEUMONIA Classification Report & memoir(회고)

# AIFFEL Online Core 6기 최현우

## Flow Chart
<시간이 없어 로컬 이미지 올리는 법을 못 찾았습니다! 깃헙에 링크로 올리겠습니다>

[Flow Chart IMAGE](https://github.com/HWMV/AIFFEL_Quest1/blob/master/Main_quest/Main_quest4/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202023-11-09%20%EC%98%A4%ED%9B%84%205.06.39.png)

---
## 1. Use model
* ResNet18 model 구현
* Risidual Learning : Skip Connection(identity_block) 기법 활용
* Data input size : 180, 180, 3
* Classification Class : NORMAL(정상), PNEUMONI(폐렴)

## 2. Model Architecture
* skip connection의 기법을 담은 'identity_block' function
  * (X 이전레이어, f 필터크기, filters 채널 수)를 인자로 받고 X_shortcut = X로 Skip Connection을 정의 했습니다. 각 stage 마다 BottleNeck(1x1)로 연산량을 감소시키고, 다음 stage2,3은 이전 레이어의 필터를 받고 Conv를 진행한 후 final step에서 Skip connection과 이전 레이어를 합치고 출력 합니다 

* ResNet의 뼈대 Layer를 담은 'ResNet18' function
  * input을 받고 7x7 층을 통과하여 사이즈를 줄이고, stage 별로 [64,128,256,512] 채널 수를 깊게하며 사이즈를 감소 시킵니다. stage 별로 Conv 층 수는 [3,4,6,5]개씩 구성하였습니다. 마지막 층에서 GlobalAvgPooling을 적용하고 FC 레이어를 통해 출력 하였습니다. 이진분류 task여서 출력 활성화함수는 'sigmoid'로 하였습니다

  (참고 블로그 구조 이미지가 각 stage 별로 Conv층 수가 달랐습니다)
<이미지 추가>

---
## 3. 성능 향상을 위한 기법
* Data Augmentation (Flip, ZOOM, Rotation) : 데이터 수가 적음

* Shuffle, repeat, batch, prefetch : 학습 성능을 향상 (prefetch 새로운 것 배움!)

* Data balance 처리 : val data가 상대적으로 너무 적음

* EarlyStopping : 에폭 수를 늘리면서 설정

* learning_rate_scheduler : Local, global feature 마다 학습률 연관이 있다 하여 추가

* GPU 사용 코드 적용 (새로운 것 배움)

---
## 4. 프로젝트 느낀점

새로 알게 된 코드는 (기억!)으로 체크 추후 깊게 알아볼 예정이며, 5번 노드 코드를 기본으로 최종 프로젝트에서 추가한 부분은 '##'으로 체크하였습니다.

지금까지 아이펠에서 해온 과정이 전부 녹아 있는 느낌이였습니다. 구조와 개념을 천천히 이어서 외워 가다보면 맞는 task에 활용할 수 있겠구나 느꼈습니다. 지금까지 한 공부가 빠질 것 없이 도움 되는 것에 퍼실님과 AIFFEL 과정에 감사합니다!

어려웠던 점은 데이터를 분리 해주셔서 편하였지만 나중에 스스로 데이터를 수집하고 전처리 하는 과정을 잘 해낼 수 있을지 걱정 됩니다. 이런 부분도 한번 교육과정으로 배웠으면 하는 마음이 들었습니다.

논문에 모델 구조 이미지를 보고 직접 Functional API 방식으로 구현 해보니 딥러닝을 한층 더 알게 된 기분이 들었습니다.

---
## 5. CNN & ResNet 성능 지표 비교 (시각화 사진 올리는 법을 모르겠어요)
* 추가로 계속 Test 중 입니다! (최대 ACC 82%) > (Test file Final ACC 87.5%)
  
* ResNet (Batch size를 늘리니까 성능이 계속 떨어집니다)
Loss: 0.5794280767440796,
Accuracy: 0.7964743375778198,
Precision: 0.7553398013114929,
Recall: 0.9974358677864075

* CNN
Loss: 1.3865891695022583,
Accuracy: 0.7323718070983887,
Precision: 0.7115749716758728,
Recall: 0.9615384340286255

* ResNet_Test (Epoch 끝나면 업데이트 할 예정)
Loss: 0.30288001894950867,
Accuracy: 0.875,
Precision: 0.8679245114326477,
Recall: 0.9435897469520569

---
## 6. 참고 블로그
(구조 이미지 참조)
[참고 블로그](https://wjunsea.tistory.com/99)
