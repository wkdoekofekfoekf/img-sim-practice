# img-sim-practice



## 목표 : 딥러닝 모델을 사용하여 이미지의 유사도를 비교하는 프로젝트

# 개발 환경 : NVIDIA a-100 그래픽이 탑재된 고성능 컴퓨팅 환경을 이용함

# 프레임워크 : pytorch 1.11.0+cu113 CPU 사용

# 라벨링 툴 : roboflow



# --------------------------------------- DATA ---------------------------------------

## 1. 데이터 수집 

![image](https://user-images.githubusercontent.com/62790857/212647870-6458577c-9585-48e9-8211-a336be0fad8e.png)

구글과 네이버를 통하여 이미지를 수집후 trash 파일은 삭제함.


## 2. 라벨링

![image](https://user-images.githubusercontent.com/62790857/212648098-7c0f917b-e34d-42c7-ac54-592919f5b15c.png)


앞서 기재한 roboflow 라벨링 툴을 이용해 yolov5에 맞추어 물체의 경계 상자를 만듬.

## 3. 이미지 증강

얻어낸 이미지의 양이 학습에 부족하다고 느껴 케라스의 이미지 증강 라이브러리 사용하여 각 클래스 당 1500장으로 증강함.





![image](https://user-images.githubusercontent.com/62790857/212648633-b27489f6-a40a-47be-a308-0d44c37f26f8.png)




