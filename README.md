# img-sim-practice



## 목표 : 딥러닝 모델을 사용하여 이미지의 유사도를 비교하는 프로젝트

# 모델 : yolov5
(yolov4를 사용하여 전의 프로젝트를 진행한 적이 있음. 파이토치 버전으로 새롭게 v5가 나왔다는 소식을 듣고 v5의 성능을 파악한 뒤 진행해봄.)

참조 : https://medium.com/deelvin-machine-learning/yolov4-vs-yolov5-db1e0ac7962b

# 개발 환경 : NVIDIA a-100 그래픽이 탑재된 고성능 컴퓨팅 환경을 이용함

# 프레임워크 : pytorch 1.11.0+cu113 CPU 사용

# 라벨링 툴 : roboflow



# ----------------------- DATA ------------------------

## 1. 데이터 수집 

![image](https://user-images.githubusercontent.com/62790857/212647870-6458577c-9585-48e9-8211-a336be0fad8e.png)

구글과 네이버를 통하여 이미지를 수집후 trash 파일은 삭제함.


## 2. 라벨링

![image](https://user-images.githubusercontent.com/62790857/212648098-7c0f917b-e34d-42c7-ac54-592919f5b15c.png)


앞서 기재한 roboflow 라벨링 툴을 이용해 yolov5에 맞추어 물체의 경계 상자를 만듬.

## 3. 이미지 증강

얻어낸 이미지의 양이 학습에 부족하다고 느껴 케라스의 이미지 증강 라이브러리 사용하여 각 클래스 당 1500장으로 증강함.





![image](https://user-images.githubusercontent.com/62790857/212648633-b27489f6-a40a-47be-a308-0d44c37f26f8.png)


# --------------------윤곽선 비교-----------------------

만약 객체를 탐지한 뒤 윤곽선을 추출할 수 있다면 이 두개의 윤곽선을 비교하면 유사도로 판별할 수 있을까? 생각하게 됨.


![image](https://user-images.githubusercontent.com/62790857/212654236-19c7bb66-fbc4-470b-a036-daa7c09995c2.png)


![image](https://user-images.githubusercontent.com/62790857/212654268-1c12d82d-39d2-4f95-bab6-16acfb87440b.png)



# opencv 컨투어 추출

opencv의 draw contour라는 메소드를 이용함.
검은색 배경의 흰색객체를 추출한다고 함. 
이미지를 그레이스케일화 하여 진행하였지만, 배경에 많은 영향을 가지는 것을 확인함.



# rembg 오픈소스 활용

출처 : https://github.com/danielgatis/rembg

foreground extraction에 좋은 성능을 가지고 있는 오픈 소스 딥러닝 모델임.

원본 : 
![stone (1)](https://user-images.githubusercontent.com/62790857/212655523-b69f8416-7405-4cf8-a0a3-f3e4f805bbe9.jpg)

결과 :  
![stone_out](https://user-images.githubusercontent.com/62790857/212655352-7df2625f-b6b5-4d44-9cfe-7acf72bd597f.jpg)


위와 같이 전경 추출에 효과가 있는 것을 파악함. 

따라서 이미지를 정제후 윤곽선을 비교하는 것이 좋다고 생각하여 진행하였음.

![Image1](https://user-images.githubusercontent.com/62790857/212655753-ae197832-48de-4d1c-813d-254cd1a9c4b6.png)


opencv의 matchshape 메소드를 이용하여 두 개의 사진의 윤곽선을 뽑아내어 그 윤곽선의 일치도를 결과로 도출하는 것을 원하였음.

# 그러나

윤곽선은 윤곽선 일뿐 보는 시점에 따라 같은 물체라도 윤곽선이 다르다는 것을 알 수 있었음.

결과를 도출하는 것 까지는 성공했지만, 물체를 판별하기에는 부적합 하다고 판단하여 진행을 멈춤.










