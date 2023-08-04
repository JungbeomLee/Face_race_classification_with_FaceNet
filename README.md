# Face_race_classification_with_FaceNet
> FaceNet을 사용해 사람들의 인종을 판별해 내는 프로젝트이다.


> 분류 가능한 인종
>> Northern_European, Semitic, Southern_European, West_Asian, Central_Asian, Native_American, North_Asian, Southeast_Asian, African_American, East_African, South_African, West_African
# dataset
> 이미지 생성 모델을 사용하여 직접 만든 데이터셋을 사용하였다.

> https://drive.google.com/drive/folders/1DeZWQhnxMkoiqlM8ylWB9_N4J1AMzCYF?usp=sharing

> 위 데이터셋은 상업적 이용이 가능하다.

# 원리

> 인종들의 얼굴 이미지를 Facenet을 사용하여 임베딩 한 후, 벡터들의 평균값을 구한 후, 구한 평균값을 해당 인종을 대표하는 값으로 지정한다.

> medipaipe를 이용해 사용자가 입력한 이미지에서 얼굴 영역만 크롭한 후, Facenet을 이용해 얼굴을 임베딩 한다.

> 유클리드 거리 계산법을 사용해 임베딩된 이미지의 벡터값에서 각 인종을 대표하는 벡터값의 거리 차이를 구한다.

> 거리값을 0과 1 사이의 값으로 정규화 한다. (normalized_distance = distance−min_distance/max_distance−min_distance)

> 1에서 정규화된 거리값을 뺀다.
>> 이를 통해 가장 가까운 거리가 1에, 가장 먼 거리가 0에 매핑된다.

> 마지막으로 100을 곱해 값을 퍼센테이지로 변환한다.

# FaceNet 모델 다운로드
> Hiroki Taniai가 제공하는 모델을 사용하였다.
> https://drive.google.com/drive/folders/1pwQ3H4aJ8a6yyJHZkTwtjcL4wYWQb7bn

# 사용 방법
> 'Face_race_classification_with_FaceNet.py'에 있는 'face_fair_check' Class를 사용한다.
```python
race_check = face_fair_check('--your model path')
img = race_check.get_face('--your image path')
vector = race_check.get_embedded_face(img)
race_check.get_face_race(vector, 0) #male 0, female 1
---output ex).---
{'Northern_European': 100.0,
 'Southeast_Asian': 94.18422654271126,
 'South_African': 92.66502484679222,
 'East_African': 74.67080950737,
 'West_African': 74.53552484512329,
 'Native_American': 73.30910563468933,
 'African_American': 61.952802538871765,
 'North_Asian': 46.673959493637085,
 'Central_Asian': 41.44601225852966,
 'Semitic': 22.921371459960938,
 'West_Asian': 6.444507837295532,
 'Southern_European': 0.0}
```
