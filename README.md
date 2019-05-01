# AlexNet

컴퓨터 비전 분야에서 ConvNet을 유명하게 만든 것은 Alex Krizhevsky, Ilya Sutskever, Geoff Hinton이 만든 [AlexNet](http://papers.nips.cc/paper/4824-imagenet-classification-with-deep-convolutional-neural-networks)이다. AlexNet은 [ImageNet ILSVRC challenge](http://www.image-net.org/challenges/LSVRC/2014/) 2012에 출전해 2등을 큰 차이로 제치고 1등을 했다 아키텍쳐는 LeNet과 기본적으로 유사지만, 더 깊고 크다. 또한 여러 개의 CONV 레이어들이 쌓여 있다. 

## AlexNet 특징

1. 3개의 fully-connected layer과 5개의 convolutional layer 사용

2. 2.기존 모델들과 다르게 activation function으로 Relu를 이용하여 학습시간을 매우 단축했다.

3. ReLU 적용후 Local Response Normalization 적용함(첫번째, 두번째 Convolutional Layer에만 적용).

4. pooling size =3 stride =2를 사용하여 겹치는 max pooling을 사용하였는데 이것이 오버피팅을 막는데 도움을 주었다(첫번째, 두번째, 다섯번째 Convolutional Layer에 적용). 

5. fully-connected 부분에서 뉴런이 동조화 하는것을 막기 위해 drop out을 0.5로 적용했다. 단 테스트시에 output에 0.5를 곱해주어야 한다.

6. data agum entation을 활용해 256x256이미지를 랜덤으로 227x227로 학습데이터를 늘려 오버피팅을 방지하였다.

7. ImageNet 2,000개 이상의 카테고리를 가진 레이블링된 고해상도 이미지 데이터 1500만개의 사용. 

8. 5-6일간 GTX 580 3GB GPU 2개를 가지고 학습함. 

9. 사용된 입력 이미지 사이즈는 256x256x3(RGB)로 고정하여 사용함.(256보다 작은 사이즈는 center에 위치하도록 하여 256 사이즈를 만족시킴)

10. 

    ## AlexNet의 Architecture
   
    

    [227x227x3] input layer 

    [55x55x96] Conv1

    [27x27x96] Max Pool 1

    [27x27x256] Norm 1

    [13x13x256] Max Pool 2

    [13x13x256] Norm 2

    [13x13x384] Conv 3

    [13x13x256] Conv 5

    [6x6x256] Max Pool 3

    [4096] Fully Connect 

    [4096] Fully Connect 

    [1000] Fully Connect 

    



## 사용된 CNN Architecture

1. Fully-connected layer

   Fully connected 레이어 내의 뉴런들은 일반 신경망 챕터에서 보았듯이 이전 레이어의 모든 액티베이션들과 연결되어 있다. 그러므로 Fully connected레이어의 액티베이션은 매트릭스 곱을 한 뒤 바이어스를 더해 구할 수 있다. 더 많은 정보를 위해 강의 노트의 “신경망” 섹션을 보기 바란다. 

2. ConvNet 구조

   위에서 컨볼루셔널 신경망은 일반적으로 CONV, POOL (별다른 언급이 없다면 Max Pool이라고 가정), FC 레이어로 이뤄져 있다는 것을 배웠다. 각 원소에 비선형 특징을 가해주는 RELU 액티베이션 함수도 명시적으로 레이어로 취급하겠다. 이 섹션에서는 어떤 방식으로 이 레이어들이 쌓아져 전체 ConvNet이 이뤄지는지 알아보겠다. 

3. Conv layer

   (3x3 또는 최대 5x5의)작은 필터들과 S=1S=1의 stride를 사용하며, 결정적으로 입력과 출력의 spatial 크기 (가로/세로)가 달라지지 않도록 입력 볼륨에 제로 패딩을 해 줘야 한다. 즉, F=3F=3이라면, P=1P=1로 제로 패딩을 해 주면 입력의 spatial 사이즈를 그대로 유지하게 된다. 만약 F=5F=5라면 P=2P=2를 사용하게 된다. 일반적으로 FF에 대해서 P=(F−1)/2P=(F−1)/2를 사용하면 입력의 크기가 그대로 유지된다. 만약 7x7과 같이 큰 필터를 사용하는 경우에는 보통 이미지와 바로 연결된 첫 번째 CONV 레이어에만 사용한다. 

4. Pooling layer

   ConvNet 구조 내에 컨볼루션 레이어들 중간중간에 주기적으로 풀링 레이어를 넣는 것이 일반적이다. 풀링 레이어가 하는 일은 네트워크의 파라미터의 개수나 연산량을 줄이기 위해 representation의 spatial한 사이즈를 줄이는 것이다. 이는 오버피팅을 조절하는 효과도 가지고 있다. 풀링 레이어는 MAX 연산을 각 depth slice에 대해 독립적으로 적용하여 spatial한 크기를 줄인다.  

5. Backpropagation

   컨볼루션 연산의 backward pass 역시 컨볼루션 연산이다 (가로/세로가 뒤집어진 필터를 사용한다는 차이점이 있음).  

# 출처

  출처: <https://arclab.tistory.com/156> [Arc Lab.'s Blog] <http://aikorea.org/cs231n/convolutional-networks/> 
