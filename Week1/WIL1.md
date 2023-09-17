### MLP(multi-layer-perceptron)
* Task에 따라 사용되는 Loss function이 달라진다.
    * Regression : MSE, ...
    * Classification : Cross entropy, ...
    * Probablicstic : MLE, ...

### Generlization
* Ensemble : 여러 개의 분류 모델을 조합하여 성능을 향상 시키는 기법
    * Bagging : subset을 나누어 학습 후 각각의 voting (soft/hard) 이나 averaging을 구한다(병렬적으로 학습)
    * Boosting : 학습이 제대로 되지 않은 데이터들을 모아 새로운 간단한 모델로 재학습 (순차적으로 학습)

* Regularization
    * Early Stopping
    * Parameter norm penalty
    * Data augmentation
    * Noise robustness
    * Dropout
    * Label smoothing

### CNN(Convolutional Neural Networks)
* FNN vs CNN
    * FNN은 인접 픽셀간의 상관관계가 무시되어 이미지를 벡터화하는 과정에서 정보 손실이 발생 -> 컨볼루션 연산을 통해 인접 픽셀간의 상관관계에 대한 정보를 담고 있는 Feature map을 사용
* Pooling
    * max pooling
    * average pooling
* 1*1 convolution
    * depth 의 차원을 변경 가능 -> NN을 더 깊게 쌓을 수 있다. bottle-neck 구조에서 사용