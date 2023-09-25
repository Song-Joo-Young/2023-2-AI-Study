## Semantic Segmentation
* Segmentation : 입력 이미지를 픽셀 수준으로 분석하여 각 픽셀에 클래스 레이블을 할당
    * Semantic Segmentation
      * 각 픽셀은 해당 픽셀이 어떤 객체 또는 클래스에 속하는지를 나타낸다. 
      * 모든 픽셀에 대해 **하나의 클래스 레이블이 할당**되며, **동일한 클래스에 속하는 모든 픽셀은 동일한 레이블을 공유**한다.
    * Instance Segmentation
      * Semantic segmentation과 유사하지만 더 상세한 작업이다.
      * 이미지를 픽셀 단위로 분할하는 동시에, **각 객체 또는 인스턴스를 고유하게 식별**한다. 즉, **서로 다른 객체 간에도 개별적인 분할**이 이루어진다.

* FCN vs CNN
  * CNN(Convolution Neural Network)
    * CNN은 컨볼루션 레이어를 사용해 입력 이미지를 작은 필터로 스캔하고, 이미지의 다양한 특징을 학습한 feature map을 출력으로 내보내고, 이를 FC Layer를 사용해 분류 작업을 수행하는 방식이다. 
  * FCN(Fully Convolutional Network)
    * 그런데 FC layer를 사용하면 기껏 보존해온 공간 정보가 사라진다는 문제점이 있다. 따라서 FC layer를 사용하지 않고, 컨볼루션 레이어만 사용하는 것이 CNN을 확장한 FCN이다. FCN은 픽셀 단위로 라벨을 예측하는 세그멘테이션 작업에 적합하도록 설계된 아키텍처이다. FCN은 CNN과 달리 FC layer를 사용하지 않고 컨볼루션만을 사용해 특징 추출과 분류를 모두 수행한다.
    * FCN은 feature map을 **업 샘플링(upsampling)**하여 입력 이미지와 동일한 크기의 feature map을 생성하고, 각 픽셀에 대한 클래스 예측을 수행한다. 이를 통해 픽셀 수준의 세그멘테이션 결과를 얻을 수 있다.
  
  * Object Detection
    * R-CNN
      * 1. selective search
      * 2. region size process
      * 3. Compute CNN features
      * 4. Linear SVM로 classify
    * SPPNet
      * CNN 과정을 피처값인 서브텐서만 뜯어와서 계산하는 방식으로 연산량을 획기적으로 줄인 구조.
    * Fast R-CNN
      * 1. selective search
      * 2. Compute CNN feature
      * 3. ROI Pooling : 패치들을 고정된 feature 값으로 만들기 위한 작업
      * 4. NN을 통해 bbox regressor and softmax 수행
    * Faster R-CNN
      * Fast R-CNN + **Region Proposal Network(RPN)** 개념 도입
      * Region Proposal Network(RPN)
        * selective search 알고리즘 대체
        * bbox region 또한 학습 가능한 네트워크
        * 이미지 안에 특정 영역이 bbox로 의미가 있을지 없을지 계산해주는 네트워크
    * YOLO
      * [YOLO 논문 요약](https://songsite123.tistory.com/64)
