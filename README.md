# 프로젝트 소개
<p align="center">
  <img src="https://github.com/user-attachments/assets/f31ed794-590c-4b0a-8dfe-9958e18b0b3a">
</p>
영상 분석에서 샷을 효과적으로 구분하기 위한 샷 경계 검출은 영상 분석 외에도 콘텐츠 요약, 편집 자동화 등의 다양한 응용 분야에서 요구되는 중요한 전처리 과정입니다.<br>
기존 히스토그램 상관계수 기반 샷 경계 검출 방식이 색상 변화나 배경 효과로 인해 잘못된 샷 경계를 검출하는 문제를 해결하기 위해, YOLOv8 기반 객체 탐지 기법을 결합한 새로운 샷 경계 검출 방법입니다.<br>

# 핵심 기능 소개
## 1. 샷 경계 후보군 검출
1) 샷 경계 후보군을 검출하기 위해 이미지의 RGB 채널별 색상 히스토그램을 활용하여 연속된 프레임 사이의 히스토그램 상관계수를 계산합니다.<br>
2) 히스토그램 상관계수가 임계값 보다 낮은 경우 샷 경계 후보군으로 지정합니다.<br>

## 2. YOLOv8을 활용한 샷 경계 확정
1) 샷 경계 후보 프레임들에 대해 YOLOv8을 적용하여 사전 학습된 80개의 클래스에 해당하는 객체들을 탐지합니다.<br>
2) 두 프레임에 나타난 객체의 변화 정도를 객체간 IoU계산을 활용하여 측정 후, 변화 정도가 큰 경우 샷의 경계로 확정짓습니다.<br>
3) 이때 프레임에 나타난 객체들 간의 IoU를 계산하기 위해 객체간 매칭에 헝가리안 알고리즘을 활용합니다.<br>

# 실험 결과
|Video Name|Metric|Histogram Correlation|Histogram Correlation + YOLOv8|
|:---|:---:|---:|---:|
|video #1|precision|0.2522|0.9565|
||recall|0.9667|0.7333|
||f1-score|0.4000|0.8302|
|video #2|precision|0.3659|0.9574|
||recall|0.9783|0.9783|
||f1-score|0.5326|0.9677|
|video #3|precision|0.6265|0.9808|
||recall|1.0000|0.9808|
||f1-score|0.7704|0.9808|
|video #4|precision|0.1557|0.8261|
||recall|0.9744|0.9744|
||f1-score|0.2686|0.8941|
|video #5|precision|0.1959|0.9180|
||recall|0.9508|0.9180|
||f1-score|0.3249|0.9180|
|video #6|precision|0.8333|0.9804|
||recall|0.8929|0.8929|
||f1-score|0.8621|0.9346|

- 밝기 및 색상의 변화와 배경의 영상 효과 변화가 큰 데이터셋을 사용하기 위해 가수의 공연 영상 6개를 이용하여 테스트하였습니다.<br>
- 객체 탐지에는 COCO 데이터셋을 기반으로 80개의 클래스를 탐지할 수 있도록 사전 학습된 YOLOv8x 모델을 사용하였습니다.
<br><br>
