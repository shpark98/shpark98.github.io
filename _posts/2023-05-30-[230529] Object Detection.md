---
published: true

layout: single

title: "[2023-05-29] Object Detection"

categories: [Devcourse-TIL]

tags: Autonomous_Driving CV

toc: true

toc_label : 목차

toc_sticky: true

author_profile: false

sidebar :
    nav : "docs"
---

## Object Detection

- Bounding Box로 Object에 대한 위치를 찾고, Bounding Box의 위치에 있는 Object를 구분하는 과정

![image](https://github.com/shpark98/Projects/assets/116723552/e9c54098-6c11-4be2-ab32-37b45e11edc3)



### Classification

- 이미지가 input으로 들어가면 CNN 모델을 통해서 output에 N개의 클래스에 대한 확률 분포가 나옴

![image](https://github.com/shpark98/Projects/assets/116723552/5e6fb47a-3539-455b-8827-4aba85423453)



### Object Localization

- Classification에서 바운딩 박스의 정보를 담는 X, Y, W, H 4개의 point 값을 추가

![image](https://github.com/shpark98/Projects/assets/116723552/e42ad074-6897-4681-907e-d4551d78c72b)



### Object Detection

- Object 수 만큼 Class에 대한 확률분포, Bounding Box 정보가 나옴
- 하나의 이미지에서 여러개의 Object를 검출할 수 있음

![image](https://github.com/shpark98/Projects/assets/116723552/f03b8c7a-57d5-4329-9478-05da61d65817)



#### Network architecture of Classification and Object Detection

### ![image](https://github.com/shpark98/Projects/assets/116723552/029e65de-b372-471e-ba98-101b972eab84)



### One Stage Detection & Two Stage Detection

- One Stage Detection은 객체의 검출과 분류, 바운딩 박스 regression을 한번에 하는 방법
- Two Stage Detection은 Object가 있을 법한 위치의 후보들을 뽑아내는 단계와 실제 Object가 있는지 확인하는 Classification과 정확한 바운딩 박스를 구하는 Regression을 수행하는 단계가 분리되어 있음



#### One Stage Detection

![image](https://github.com/shpark98/Projects/assets/116723552/a71b3976-26dc-4d3d-909f-a8ff98f54900)

<img src="https://github.com/shpark98/Projects/assets/116723552/fd707008-606c-4003-a305-488aebd821e4" alt="image" style="zoom:67%;" />

- Backbone

  - 이미지나 비디오와 같은 입력 데이터를 처리하여 중요한 특징을 추출하는 역할을 함
  - 추상적인 특징을 추출함
  - Layer가 깊어질 수록, 점점 feature map은 추상화됨

  <img src="https://github.com/shpark98/Projects/assets/116723552/24b005e2-9b28-487b-babb-a62789e14633" alt="image" style="zoom:67%;" />

  

- Neck

  - Backbone에서 추출한 특징을 가공하고 조정하여 이후의 작업을 수행하기 좋은 형태로 만듬
  - Backbone의 특징을 활용하여 보다 구체적인 작업에 유용한 표현을 생성함
  - 특징이 Concaenatete되거나 Add 됨
  - Concatenate
    - Channel로 추가가 됨
    - A matrix : [C, H, W] / B matrix : [C, H, W] 를 Concatenate 진행시 C = [2C, H, W]  (C : Channel, H : Height, W : Width)
  - Add
    - Element Wise addition 진행
    - A matrix : [C, H, W] / B matrix : [C, H, W] 를 add 진행시 C = [C, H, W]  (C : Channel, H : Height, W : Width)

<img src="https://github.com/shpark98/Projects/assets/116723552/4786eea9-21a1-4831-8cf1-626de1ea3cf5" alt="image" style="zoom:67%;" />

- Dense Prediction
  - Class에 대한 정보를 담는 개수와 Class의 확률 값과 Bounding 값이 나오는 부분





#### Two Stage Detection

- One Stage보단 정확하지만 많은 연산을 사용함

![image](https://github.com/shpark98/Projects/assets/116723552/ebe97fa6-af39-4a6b-8323-3187006e1b13)

<img src="https://github.com/shpark98/Projects/assets/116723552/222d9179-8882-476f-9aef-25f9062553b4" alt="image" style="zoom:67%;" />

- Faster R-CNN은 Two Stage Object Detector 중 하나
- 첫번째 forward 에서는 후보 영역들을 뽑음
  - Input 이미지를 CNN 을 통해 feature map을 뽑고 Object가 있을 것 같은 자리에 Region Proposal Network를 진행함
- 두번째 forward 에서는 후보 영역들 중에 인프런스를 통해 실제 Object가 있는 것을 확인

<img src="https://github.com/shpark98/Projects/assets/116723552/57f4a997-a94a-4b8b-83ff-aeb73e4dd849" alt="image" style="zoom:67%;" />





### Grid

- feature map의 pixel 수로 feature map size가 [13, 13]일 때 grid size는 [13, 13] 

<img src="https://github.com/shpark98/Projects/assets/116723552/63b93672-7493-4cd4-bfe5-49343d146395" alt="image" style="zoom: 80%;" />

- Grid 안에서 객체를 찾는 방법은?
  - Grid에서 1개의 Object를 검출하기 위해 여러가지 바운딩 박스를 만듬
  - 해당 Object의 바운딩 박스의 정보, Object 위치와 Class 정보를 내포하는 결과가 나옴

<img src="https://github.com/shpark98/Projects/assets/116723552/ab51a43b-c2ec-4aca-b71b-0161d3bb3f81" alt="image" style="zoom:67%;" />



### Anchor

- 사전에 정의된 크기와 종횡비(가로 대 세로 비율)를 가지고 있는 상자
- Anchor Box는 이미지 내에 존재할 가능성이 있는 객체의 위치와 크기를 대략적으로 나타냄

<img src="https://github.com/shpark98/Projects/assets/116723552/4f6acf7e-e40f-4fee-9f13-c62815832e1c" alt="image" style="zoom:67%;" />

- 앵커가 5개 있을 때
  - Box Offset(4) + Objectness_confidence(1) + Class_confidence(20) = 25개 원소
  - 총 125개의 channel을 갖는 feature map이 됨

![image](https://github.com/shpark98/Projects/assets/116723552/fc95f185-b7ec-484f-8143-5f42f4a754d5)





### Bounding Box, Objectness Score, Class Score

- Bounding Box
  - [x_min, y_min, x_max, y_max]  or [x_center, y_center, w, h]
- Objectness Score
  - Object라고 판단되지 않는 것들은 0으로 주고 Object 라고 판단되는 것은 1 줌
- Class Score
  - 각 클래스별로 GT를 구분하고 객체에 대한 클래스를 예측함

<img src="https://github.com/shpark98/Projects/assets/116723552/49ed970e-2f5a-46b9-aa01-a59179b69b95" alt="image" style="zoom: 80%;" />





### Loss Function



#### Softmax

- 예측한 클래스의 Score의 합을 1로 만드는 과정 

<img src="https://github.com/shpark98/Projects/assets/116723552/c2223db9-c05e-413d-95f6-3e8658a23498" alt="image" style="zoom:67%;" />



#### Cross-Entropy Loss

- 분류 모델의 출력과 실제 레이블 간의 차이를 측정하여 모델의 학습을 도와줌

<img src="https://github.com/shpark98/Projects/assets/116723552/121e5a8a-2527-41df-8fb4-c8214f7827f6" alt="image" style="zoom:67%;" />

#### MSE loss, MAE loss

![image](https://github.com/shpark98/Projects/assets/116723552/947b16a3-854a-407e-aa1e-82fc7a803757)





### IOU

- Intersection over Union

![image](https://github.com/shpark98/Projects/assets/116723552/98c4265a-c271-4e3b-a488-0de518fb53c3)



### NMS

- Non - Maximum Suppression

- IOU와 Confidence Score을 기준으로 필터링함

<img src="https://github.com/shpark98/Projects/assets/116723552/1e20f50a-201c-432e-9ac8-4684fac80e47" alt="image"  />





## Object Detection Models



### One-Stage Object Detectors

- YOLO(You Look Only Once)

- SSD(Single Shot Detectors)



### Two-Stage Object Detectors

- RCNN
- Fast-RCNN
- Faster-RCNN
