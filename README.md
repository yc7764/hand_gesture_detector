# hand_gesture_detector
## 프로그램 개요
  카메라를 통해 실시간으로 손동작을 입력 받으면 수화 의미를 분류하는 프로그램.
  직접 학습시킨 모델을 이용해서 실시간 이미지 데이터를 분류.
  정지된 이미지의 수화가 아닌 동작을 의미하는 수화들을 분류할 수 있다는 점에서 작품성이 있다.

## 프로그램 환경
  개발도구 – Python3.7.3, Jupyter notebook
  Package  - tensorflow, keras, mediapipe, LSTM, openCV …

## 프로그램 흐름도
  1. 카메라를 이용해서 실시간으로 영상을 입력 받는다.
  2.  얼굴, 포즈, 손을 인식해서 keypoint를 구한다. Keypoint는 x,y,z위치 정보를 가진다.
  3.  keypoint를 이용해서 동작을 예측한다.
  
![image](https://user-images.githubusercontent.com/59434021/187091843-475ec7d0-1c6d-419f-966c-fb8b70baceb2.png)

## 학습데이터
  - 수화를 의미하는 학습데이터를 직접 생성<br/>
  - 학습데이터는 left-hand, right-hand, pose의 keypoint들로 이루어져있다.<br/>
  - 30 frame을 1 sequence로 설정 <br/>
  - 수화 하나당 약 200개의 sequence data를 생성 <br/>
  - 총 78,000개의 학습데이터 생성(200x13x30)<br/>
  
## 신경망 설계 
 - LSTM 구조 신경망
 - 긴 시퀀스의 입력을 처리하는데 좋음
 - 입력층의 크기 258*학습데이터 수, 출력층의 크기 13개
 
## 신경망 모델 성능 평가
![image](https://user-images.githubusercontent.com/59434021/187091485-0d943255-5902-417a-89de-eab54142e42c.png)

| gesture  | accuracy | gesture   | accuracy |
|----------|----------|-----------|----------|
| yes      | 99%      | do it     | 100%     |
| no       | 99%      | glad      | 99%      |
| hate     | 97%      | good      | 98%      |
| don't    | 99%      | bad       | 99%      |
| fine     | 99%      | tired     | 100%     |
| sorry    | 100%     | follow me | 100%     |
| let's go | 99%      |           |          |
 
## 프로그램 UI
  - 분류된 수화 의미를 화면 상단에 텍스트로 출력 
  - 이전에 분류했던 수화 의미를 5개까지 출력해주면 왼쪽에서 오른쪽 순서대로 업데이트하여 출력
  - 분류할 때 가장 높은 확률을 가진 두개의 수화 의미와 확률을 왼쪽 상단에 출력
![image](https://user-images.githubusercontent.com/59434021/187092548-c7cdf873-27ad-4244-8b78-1ca47b75dcee.png)
