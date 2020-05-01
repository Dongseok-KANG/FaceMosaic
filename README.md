# FaceMosaic

2019-1 경기대학교 데이터마이닝 팀 프로젝트 (19.05 ~ 19.06)

CNN 알고리즘을 활용한 영상 자동 모자이크 시스템

사용 라이브러리 : OpenCV, Tensorflow
## 아이디어 제안 배경
이전 통계자료분석대회의 연장선으로 진행한 프로젝트로, 당시 사회적 문제로 화두가 되었던 '몰카' 즉 초상권 문제에서 아이디어를 도출해냈다.

### 초상권 침해
스마트폰, 카메라 등의 촬영 기능을 가진 전자기기가 대중화되면서, 타인의 사진이나 영상에 얼굴이 노출이 되는 
'초상권 침해 문제'가 심각한 사회적 문제로 야기되고 있다. 최근 서울시의 경우 '동의 없이 촬영, 유포한 영상에서 특정인을 식별할 수 있는 얼굴
등이 드러날 경우 엄연한 초상권 침해 범죄로 처벌받을 수 있다' 고 밝혔다.

### 플랫폼의 활성화
또한 1인 미디어의 성장으로, 다양한 플랫폼에서 실시간 라이브 방송과 Vlog등의 야외 방송 컨텐츠가 증가하였다.
미디어 컨텐츠에서 보행자들은 본인이 인지하지 못하는 사이에 여러 경로로 자신의 얼굴이나 신체가 노출되는 상황이 발생한다.

한 두명의 얼굴 노출은 다양한 편집 툴을 이용해서 모자이크 처리가 가능하지만 다수의 얼굴 노출 또한 일일이 수작업으로 모자이크 처리를 해야 하기 때문에
편집 시 소비되는 시간이 만만치 않다. 

또한 실시간 스트리밍 방송에서는 모자이크 적용이 불가하기 때문에 실시간으로 보행자들의 초상권을 보호해줄 자동 모자이크 시스템이 필요하다.

## 분석 목적
앞서 설명한 배경을 토대로 '보행자의 초상권을 보호하기 위한 모자이크 시스템' 생성을 목적으로 분석을 진행한다. 분석에서 생성한 모델을 통해 카메라 기능을 가진 기기와 영상 편집에 적용시켜 초상관 보호에 도움을 
줄 수 있다.

## OpenCV를 이용한 1차 얼굴 식별
팀원 중 1명의 얼굴을 모델로 라벨링 작업을 실시하였다.
단순한 색이 아닌 명도를 사용해, 모델의 얼굴 이미지를 흑백으로 전환하였다.
흑백으로 전환된 이미지에서 '얼굴'을 탐지하고, 추후 CNN 분류기 적용을 위해 다시 원래 이미지 색으로 전환하였다.
![image](https://user-images.githubusercontent.com/52941937/80816336-51504c80-8c0a-11ea-8f80-b0521ab0e0a0.png)
(작성자 본인의 얼굴이 아니기 때문에, 노란색 동그라미로 가려놓았다.)

얼굴 이미지를 탐지하여, 이미지를 임의로 지정한 배율로 축소 후 모자이크 처리한다.
그 후 모자이크 이미지를 원래 크기로 복구한 후 기존이미지에 적합하는 과정을 거친다.
(이 과정에서는 특정 모델의 얼굴만 인식하는 것이 아닌, 모든 '사람'의 얼굴을 모두 인식한다.)

## CNN을 이용한 얼굴이미지 분류
CNN 학습을 위해, 
