### Object Detection
* 이미지 내에서 여러 객체 또는 물체의 위치와 클래스를 식별하는 작업
* 이미지 내의 여러 객체에 대한 정보를 제공하며, 각 객체의 위치와 클래스를 예측한다.
* vs Image Classification
  * classification 모델은 이미지가 하나의 클래스에 속하는지 결정하므로, **단일 클래스 레이블**이다. 이 때 출력은 각 클래스에 대한 확률이나 score로 나타낸다.
  * Object detection 모델은 이미지 내의 여러 개의 객체를 찾고, **각 객체에 대한 클래스를 예측**한다. **출력은 주로 Bounding box와 클래스 레이블로 구성**된다.
  
#### Location Information
* Single Location Information
  * 이미지 내의 **특정 객체 또는 물체**의 위치를 나타내는 정보를 뜻하고, 위치를 (x,y) 좌표로 표현할 수 있다. 혹은 객체의 bounding box를 사용해 위치와 크기를 나타내기도 한다. 객체 검출(object detection) 같은 작업에서 주로 사용된다.
* Multi Location Information
  * 이미지 내에서 **여러 객체 또는 물체**의 위치를 나타내는 정보이다. 이 정보는 각 객체의 위치와 **클래스를 식별**하는데 사용된다. 다중 위치 정보를 얻기 위해 여러 객체를 식별하고, 각 객체에 대한 위치와 클래스 정보를 수집하는데 이는 객체 검출 및 객체 추적(object tracking) 같은 작업에서 사용된다.


#### Sliding Window
* 컴퓨터 비전 및 객체 검출과 같은 영역에서 사용되는 기술로, 이미지 내에서 객체를 찾거나 특성을 추출하기 위한 방법 중 하나
* 이미지를 고정 크기 또는 다양한 크기의 윈도우 (부분 이미지)로 분할하고, 각 윈도우를 이동시켜 객체를 탐지하거나 특성을 추출하는 것을 의미한다.
* 동작 방식
  1. 윈도우 크기 및 이동
     *  Sliding Window은 보통 정사각형 또는 직사각형 모양의 윈도우를 사용
     *  윈도우는 이미지 내에서 시작 위치에서부터 일정한 간격으로 이동하면서 이미지를 순회. 간격은 보통 윈도우의 크기나 스텝 크기로 지정된다.
  2. 탐지 또는 특성 추출
     * Sliding Window를 사용하는 주요 목적은 객체를 탐지하거나 이미지에서 특성을 추출하는 것
     * 객체 탐지의 경우, 윈도우를 이미지 위로 이동시키면서 각 위치에서 객체의 존재 여부를 판단하고, 객체가 있는 위치를 감지
     * 특성 추출의 경우, 각 윈도우에서 이미지의 일부를 자르고, 해당 부분에서 특성 (예: 컬러, 텍스처, 엣지 등)을 추출하여 이미지의 특성을 표현
  3. 스케일 변화
     * 일반적으로 객체가 다양한 크기와 종횡비로 나타날 수 있으므로, Sliding Window를 여러 다른 크기로 조절하여 스케일 변화에 대응할 수 있다.
* 그러나 이 방법은 계산 비용이 많이 들고, 중복 계산이 많이 발생한다. 또한 다양한 크기의 종횡비의 객체에 대응하기 위해 여러 스케일에서 실행해야 한다. 비효율적임.

#### Region Proposal
* 계산이 너무 많아 모든 경우의 수를 따질 수 없다. 어떻게 하면 객체를 포함할 확률이 높은 이미지 영역을 찾을 수 있는가?
  * Candiate Region 만들기
  * Selective Search
  * 신경망으로 대체 (RPN, Region Proposal Network)

#### R-CNN
Region-Based CNN
1. selective search로 ROI(Region of Interest) 뽑기
2. region size process (224x224로 warping)
3. Compute CNN features
4. Linear SVM로 classify

#### IOU( Intersection over Union)
* bbox 비교 방법
* IOU가 1에 가깝다 = 같은 object를 가르키고 있을 확률이 높다.
* threshold 는 유저가 직접 정한다.

#### Non-Max Suppression (NMS)
* 겹치는 bbox를 지우는 방법
1) 가장 높은 score를 가진 박스를 선택
2) 나머지 score를 가진 박스들과 IOU를 비교하여 threshold (ex. 0.7) 이상의 IOU를 가
진 박스들을 제거
3) 무한 1,2 반복
* 문제 : 애초에 사진안에 있는 객체들이 겹쳐있는 상황인 경우 좋은 bbox를 제거하기도 함
#### Mean Average Precision (mAP)
Object Detector를 평가하는 기준
• 각 category별 Average Precision의 평균
 1) test image를 detector에 넣고 동작시킨다.
 2) NMS를 가지고 overlapping된 bbox들을 제거한다.
 3) 각 카테고리별 Average Presion을 계산한다. (Precision vs Recall Curve)
 * $$ mAP = \dfrac{1}{n} \sum_{k=1}^{k=n}AP_k \quad where \quad AP_k = the \ AP \ of\  class\  k , \ \ n = \ the \ number \ of \  classes $$ 
* threshold의 설정에 따라 정밀도와 재현율 값이 변화한다.
  * threshold 값이 높으면 bbox 수가 적어짐 (신중해짐)
  * threshold 값이 낮으면 bbox 수가 많아짐 (bbox 난사)
* Precision vs Recall Curve 
    * Precision: 모델이 positive라고 예측한 것 중에서 실제 True인 비율
    * Recall: 실제 맞게 예측한 것 중에서 모델이 Positive라고 예측한 비율
#### Fast R-CNN
* 더 자세한 내용은 추후 논문 리뷰
#### Faster R-CNN
* 더 자세한 내용은 추후 논문 리뷰
