# CNN을 이용한 IMDb 리뷰 평가
## CNN for text classification
● 문장이 주어졌을 때, 해당 문장이 정해진 label 중 어디에 속하는지 분류하는 문제이다.  
● [Kim et al., 2014]에 의하면, CNN이 text 처리에서도 잘 작동하는 것을 보여준다.  

 
<img src="https://user-images.githubusercontent.com/98728682/153190257-3db05742-52ba-4b8e-a629-d1dacdb4a220.jpeg" width="650" height="250">

## 텍스트와 Conv1d
● 텍스트는 단어 단위로 상 -> 하의 방향으로 재 정렬 되어 네트워크에 들어간다고 이미지를 그린다.  
● 단어는 그 자체로 들어가는게 아니라 특정 숫자들의 형태로 들어간다.  
● 이 숫자들의 정렬을 [channel] x [height] x [1]로 취급  
● 1은 width에 해당하며 값이 1이기 때문에 width 방향의 dimension은 무시한다.  
● 텍스트는 Conv1d filter를 사용한다.

<img src="https://user-images.githubusercontent.com/98728682/152477169-f3fd931d-56d3-4c20-9cc0-3bce43e0e688.png" width="320" height="250"><img src="https://user-images.githubusercontent.com/98728682/152477142-625fd2f2-20c8-4dae-8ff6-852915f0aed1.png" width="300" height="220">  
## 
<img src="https://user-images.githubusercontent.com/98728682/152665929-12dbd78f-41ce-40ea-84f0-4581dac0116d.png" width="780" height="500">
● 벡터 형태로 들어간 숫자들은 Conv1d filte를 거친 뒤 들어간 뒤, 다시 pooling 과정을 거친다.  

\
● pooling된 features들은 fully connected 과정을 거치고 positive, negative의 output을 도출해낸다.  

## Model overview

<img src="https://user-images.githubusercontent.com/98728682/152665707-86c54d4b-49b3-4877-a4c7-be1f5501e366.png" width="620" height="350">  

## 평가

● 평가는 선별된 IMdB 데이터셋을 사용하여 CNN 모델에 아래의 파라미터를 대입하여 진행하였다.  

● filter size마다 각각 다른 number를 대입하면, 더 좋은 정확도를 얻을 수 있다.    

● 특히 3짜리 filter에 큰 숫자를 대입하면, 더 좋은 정확도를 얻을 수 있다. 

● 학습에서 learning rate를 0.001에서 가장 좋은 정확도를 나타냈다.  

● 학습에서 가장 높게 나온 정확도는 88.9%로 나타났다.  

## 
|num_epochs|batch_sizee|num_classes|max_length|vocab_size|embedding_dim|filter_sizes|filter_counts|dropout_rate|learning_rate|evaluate_per_steps|accuracy| 
|---|---|---|---|---|---|---|---|---|---|---|---|  
|10|50|2|256|50000|300|(3,4,5)|(100, 100, 100)|0.0|0.001|100|87.5%|  
|10|50|2|256|50000|300|(3,5,7)|(500, 300, 50)|0.0|0.0005|100|87.8%|
|10|50|2|256|50000|300|(3,5,7)|(500, 300, 50)|0.0|0.001|100|88.9%| 
