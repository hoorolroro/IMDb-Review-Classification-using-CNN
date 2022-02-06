# CNN을 이용한 IMDb 리뷰 평가
## CNN for text classification
● 문장이 주어졌을 때, 해당 문장이 정해진 label 중 어디에 속하는지 분류하는 문제이다.  
● [Kim et al., 2014]에 의하면, CNN이 text 처리에서도 잘 작동하는 것을 보여준다.  

 
<img src="https://user-images.githubusercontent.com/98728682/152473514-32f5dea4-94f5-4ef3-a8f4-82897525f4c0.png" width="320" height="250">

## 텍스트와 Conv1d
● 텍스트는 단어 단위로 상 -> 하의 방향으로 재 정렬 되어 네트워크에 들어간다고 이미지를 그린다.  
● 단어는 그 자체로 들어가는게 아니라 특정 숫자들의 형태로 들어간다.  
● 이 숫자들의 정렬을 [channel] x [height] x [1]로 취급  
● 1은 width에 해당하며 값이 1이기 때문에 width 방향의 dimension은 무시한다.  
● 텍스트는 Conv1d filter를 사용한다.

<img src="https://user-images.githubusercontent.com/98728682/152477169-f3fd931d-56d3-4c20-9cc0-3bce43e0e688.png" width="320" height="250"><img src="https://user-images.githubusercontent.com/98728682/152477142-625fd2f2-20c8-4dae-8ff6-852915f0aed1.png" width="300" height="220">  

● 벡터 형태로 들어간 숫자들은 Conv1d filte를 거친 뒤 들어간 뒤, 다시 pooling 과정을 거친다.  
● pooling된 features들은 fully connected 과정을 거치고 positive, negative의 output을 도출해낸다.  
#
<img src="https://user-images.githubusercontent.com/98728682/152665668-d080fd86-513b-49f5-a86d-ce360f44d8be.png" width="780" height="500">
## Model overview

<img src="https://user-images.githubusercontent.com/98728682/152665707-86c54d4b-49b3-4877-a4c7-be1f5501e366.png" width="620" height="350">

## 프로그램 구현

● 선별된 IMdB 데이터 셋과 실제 IMdB 데이터 셋 두 가지를 학습하고 평가한다.  

● Embedding 차원은 300, filter size 3, 4, 5로 Number of filter는 각각 100개로 학습을 진행하였다.  

● 학습된 모델로 실제 IMDb 데이터를 평가해본 결과 정확도가 81.33%가 나왔다.
