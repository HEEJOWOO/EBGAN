# EBGAN : https://arxiv.org/pdf/1609.03126.pdf

#### <I studied while referring to various sites, but it is not enough. Thanks anytime for feedback.>
### <heejo5@naver.com>

Energy Based GAN
----------------
![image](https://user-images.githubusercontent.com/61686244/94901193-3479b700-04d1-11eb-88d5-9a74b2e67fe4.png)

EBGAN Loss Function과 Optimality
--------------------------------
![image](https://user-images.githubusercontent.com/61686244/94901273-5b37ed80-04d1-11eb-8c4c-abd569619f29.png)
* 정답 클래스가 정답이 아닌클래스보다 크게 되면 loss를 0으로 주는 hinge loss와 비슷한 기능을 하는 margin m
* 이렇게 손실함수를 잡게되면 Nash Equilibrium이 존재하게 되고 그때의 Value Function값이 존재
* Nash Equilibrium은 게임에 참여하는 모든 사람들이 현재선택한 방법이 선택할 수 있는 모든 방법들보다 더 좋거나 같은 상황이 유지되는 상황
* V(G,D)가 의미하는 것은 D의 Loss를 모든 data에 대하여 그리고 모든 z에 대하여 합산한 값이고, U(G,D)가 의미하는 것은 G의 Loss를 모든 z에 대해서 합산한 것을 의미

Nash Equilibrium을 이루는 최적의 G와 D
------------------------------------
![image](https://user-images.githubusercontent.com/61686244/94901546-c2ee3880-04d1-11eb-96c1-a3b516233b50.png)
![image](https://user-images.githubusercontent.com/61686244/94901675-f8932180-04d1-11eb-8551-a806968aa0f4.png)
![image](https://user-images.githubusercontent.com/61686244/94901718-0779d400-04d2-11eb-9670-3d78ebee9e0d.png)

* 첫 번째로 G,D의 최적의 값 V가 =m 이라는 것을 증명하기위해 앞에서 보여드린 V(G,D)의 식을 가져와 L_D의 값을 그대로 value Function에 대입을 하게 되면 분배 법칙에 의해서 식 5를 만들 수 있고, 노이즈 z는 최적의 G의 상황 때문에 합쳐 저서 식 6으로 만들 수 있음
* 식 6의 data의 확률을 a로 최적의 G의 확률을 b로 D를 x로 두고 치환하게 되면 ay+b(m-y)로 표현을 할 수 있음

EBGAN Architecture
------------------
![image](https://user-images.githubusercontent.com/61686244/94901800-28422980-04d2-11eb-9b05-d2ce77c6e8bb.png)
* Auto-Encoder 구조는 Energy-based Model을 표현하기 위한 대표적인 방법
* Auto Encoder로 구성된 EBGAN의 모델이 Data의 Real Img를 최대한 모방하려고 학습하면, D는 Data의 Manifold를 예측할 수 있음
* 따라서 D가 Reconstruction을 잘 하는 입력이라는 것은 Manifold상 낮은 E를 가지는 입력이라고 볼 수 있음
* D가 input을 판단하기 위해 확률적인 계산으로 하나의 비트를 사용하는 것과 달리, Reconstruction Based output은 D에게 더욱 다양한 Target을 제공
* 기존 D에 Binary Logistic Loss를 사용할 때는 0, 1 en 방향의 Target로만 트레이닝 할 수 있었지만, 이에 비해 Recopnstruction Loss는 더욱 다양한 값을 가지게 되고 gradien에 다양한 방향을 줄 수 있습니다 이말은 더 큰 Batch size를 사용한 트레이닝이 가능해짐
* D부분의 Auto Encoder가 Reconstruction을 잘 할 경우 D의 출력, 즉 입력에 대한 E는 낮아짐
* Auto Encoder가 G의 output을 잘 복원했기에 Data Distribution이 비슷해져 밀도가 높고 E는 낮게됨

Regularizer
-----------
![image](https://user-images.githubusercontent.com/61686244/94902110-a4d50800-04d2-11eb-911f-5b5229ac20c7.png)

MNIST / GAN, EBGAN 안전성 실험 / 측정 방법 : Inception score
------------------------------------------------------------
![image](https://user-images.githubusercontent.com/61686244/94902249-d221b600-04d2-11eb-92e5-31c7cf3d4908.png)
![image](https://user-images.githubusercontent.com/61686244/94902302-e4035900-04d2-11eb-8723-10503d59a38d.png)

LSUN
----
![image](https://user-images.githubusercontent.com/61686244/94902321-ee255780-04d2-11eb-8649-2b4a896bd8e4.png)

CelebA
------
![image](https://user-images.githubusercontent.com/61686244/94902347-fb424680-04d2-11eb-9cde-18999b388767.png)

ImageNet 잔디, 바다, 산, 건물
-----------------------------
![image](https://user-images.githubusercontent.com/61686244/94902452-23ca4080-04d3-11eb-874e-09555d11bfaa.png)

Conclusions
-----------
* 기존의 GAN과는 다르게 결과를 확률로 나타내지 않고 E로 나타냈다라는점
* 간단한 Hinge Loss를 사용했을 때 이 모델이 수렴한다는 것에 대한 증명
* D를 Auto-Encoder 구조로 놓고, E를 Reconstruction Error로 본 EBGAN의 Frame Work 제안
* EBGAN뿐만 아니라 일반적인  GAN에 둘 다 효과적인 모델구조와 Hyper-Parameter
* ImageNet DataSet 기반으로 256x256의 높은 해상도 img를 생성하는 EBGAN Model


