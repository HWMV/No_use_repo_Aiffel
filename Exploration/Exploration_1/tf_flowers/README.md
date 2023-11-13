<<<<<<< HEAD
<<<<<<< HEAD
# AIFFEL Campus Online Code Peer Review Templete
- 코더 : 최현우
- 리뷰어 : 서승호


# PRT(Peer Review Template)
- [o]  **1. 주어진 문제를 해결하는 완성된 코드가 제출되었나요?**
- 완성된 코드가 잘 제출되었습니다!
  
    - 문제에서 요구하는 최종 결과물이 첨부되었는지 확인
    - 문제를 해결하는 완성된 코드란 프로젝트 루브릭 3개 중 2개, 
    퀘스트 문제 요구조건 등을 지칭
        - 해당 조건을 만족하는 코드를 캡쳐해 근거로 첨부
    
- [o]  **2. 전체 코드에서 가장 핵심적이거나 가장 복잡하고 이해하기 어려운 부분에 작성된 
주석 또는 doc string을 보고 해당 코드가 잘 이해되었나요?**
- 주석도 잘 작성되어있습니다.

    - 해당 코드 블럭에 doc string/annotation이 달려 있는지 확인
    - 해당 코드가 무슨 기능을 하는지, 왜 그렇게 짜여진건지, 작동 메커니즘이 뭔지 기술.
    - 주석을 보고 코드 이해가 잘 되었는지 확인
        - 잘 작성되었다고 생각되는 부분을 캡쳐해 근거로 첨부합니다.
        
- [o]  **3. 에러가 난 부분을 디버깅하여 문제를 “해결한 기록을 남겼거나” 
”새로운 시도 또는 추가 실험을 수행”해봤나요?**
- 테스트 버전을 여러가지로 나눠서 기록을 잘 남겼습니다.
- 에폭이나 중간중간의 파라미터 값을 변형시켜서 여러가지 테스트를 하였습니다

  
    - 문제 원인 및 해결 과정을 잘 기록하였는지 확인
    - 문제에서 요구하는 조건에 더해 추가적으로 수행한 나만의 시도, 
    실험이 기록되어 있는지 확인
        - 잘 작성되었다고 생각되는 부분을 캡쳐해 근거로 첨부합니다.
        
- [o]  **4. 회고를 잘 작성했나요?**
- 리포트를 통해서 회고를 작성하였습니다.


    - 주어진 문제를 해결하는 완성된 코드 내지 프로젝트 결과물에 대해
    배운점과 아쉬운점, 느낀점 등이 기록되어 있는지 확인
    - 전체 코드 실행 플로우를 그래프로 그려서 이해를 돕고 있는지 확인
        - 잘 작성되었다고 생각되는 부분을 캡쳐해 근거로 첨부합니다.
        
- [o]  **5. 코드가 간결하고 효율적인가요?**
- 효율적인 코드입니다!

    - 파이썬 스타일 가이드 (PEP8) 를 준수하였는지 확인
    - 하드코딩을 하지않고 함수화, 모듈화가 가능한 부분은 함수를 만들거나 클래스로 짰는지
    - 코드 중복을 최소화하고 범용적으로 사용할 수 있도록 함수화했는지
        - 잘 작성되었다고 생각되는 부분을 캡쳐해 근거로 첨부합니다.


# 참고 링크 및 코드 개선
```
# 코드 리뷰 시 참고한 링크가 있다면 링크와 간략한 설명을 첨부합니다.
# 코드 리뷰를 통해 개선한 코드가 있다면 코드와 간략한 설명을 첨부합니다.
```
=======
# Exploration 01 Report
# Test Final 파일만 보시면 됩니다!

### 온라인 코어 6기 최현우


### Test 06까지 다양한 하이퍼 파라미터 조절 시 성능 변화 입니다
### review 파일은 따로 만들었습니다.

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


=======
# Exploration 01 Report
# Test Final 파일만 보시면 됩니다!

### 온라인 코어 6기 최현우


### Test 06까지 다양한 하이퍼 파라미터 조절 시 성능 변화 입니다
### review 파일은 따로 만들었습니다.

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


>>>>>>> edb8ffd58e71e23946f42759f34dd86fee6a3393
# pre-trained model 영향 순위
  1. 적절한 모델을 사용하기
  2. 데이터의 양과 질
  3. Fine_Tune
  4. LrS 조절
<<<<<<< HEAD
  5. earlystopping, epoch 조절
>>>>>>> edb8ffd (Exploration1)
=======
  5. earlystopping, epoch 조절
>>>>>>> edb8ffd58e71e23946f42759f34dd86fee6a3393
