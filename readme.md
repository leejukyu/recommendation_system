## 1. 유형
#### 1) [콘텐츠 기반 필터링](contents_based_recommener.ipynb)
- 사용자가 특정한 아이템을 매우 선호하는 경우, 그 아이켄과 비슷한 콘텐츠를 가진 다른 아이템을 추천하는 방식
- ex) 영화 추천
#### 2) 협업 필터링
- 평점 정보나 상품 구매 이력과 같은 사용자 행동 양식만을 기반으로 추천을 수행하는 것
- 사용자-아이템 평점 매트릭스와 같은 축적된 사용자 행동 데이터를 기반으로 아직 평가하지 않은 아이템을 예측 평가
- 다차원 행렬, 희소 행렬
###### (1) [최근접 이웃 협업 필터링](item-based_collaborative_filtering.ipynb)
- 메모리 협업 필터링이라고도 하며, 일반적으로 사용자 기반과 아이템 기반으로 다시 나뉨(행과 열이 바뀜)
- 사용자 기반 : 비슷한 고객들이 다음 상품도 구매
- 아이템 기반 : 이 상품을 선택한 고객들이 다음 상품도 구매
- 특정 사용자와 타 사용자 간의 유사도를 측정한 뒤 가장 유사도가 높은 TOP-N 사용자를 추출해 추천
- 사용자 기반보다는 아이템 기반 협업 필터링이 정확도가 더 높음
###### (2) [잠재 요인 협업 필터링](SGD.ipynb)
- 행렬 분해 : 대규모 다차원 행렬을 SVD와 같은 차원 감소 기법으로 분해하는 과정에서 잠재 요인을 추출
- 행렬 분해 기법을 이용해 사용자-잠재 요인행렬과 아이템-잠재요인행렬의 전치 행렬로 분해된 데이터 세트를 다시 내적곱으로 결합하여 예측
## 2. 행렬 분해
- M개의 사용자행과 N개의 아이템열을 가진 평점 행렬 R은 M X N 차원으로 구성
- 행렬 분해를 통해서 사용자-K차원 잠재요인 행렬 P(M X K)와 K차원 잠재요인-아이템 행렬 Q.T(K X N)로 분해
- 주로 SVD방식을 이용하지만 NaN값이 없는 행렬에만 적용하므로 사용 X -> 확률적 경사 하강법, ALS으로 SVD수행
##### 확률적 경사 하강법
- P와 Q행렬로 계산된 예측 R 행렬 값이 실제 R 행렬 값과 가장 최소의 오류를 가질 수 있도록 반복적인 비용 함수 최적화를 통해 츄누
- L2 규제를 반영해 실제 R 행렬 값과 예측 R 행렬 값의 차이를 최소화 하는 방향성을 가지고 최적화된 예측 R을 구함
