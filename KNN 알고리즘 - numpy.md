## KNN 알고리즘

![image-20220825170041311](https://user-images.githubusercontent.com/97595340/188319859-7ffcc135-d355-44a2-a031-a80c9c4c5930.png)

* 분모 = K명의 사람과 유사도 시그마
* 분자 = K명의 사람과 유사도 * 비슷한 사람이 준 평점을 곱한것의 시그마

고객 u가 평점을 주지 않았던 영화들 중에서 평점이 가장 높은 영화를 추천

![image-20220825170535837](https://user-images.githubusercontent.com/97595340/188319869-97a101c4-e5b2-4bad-90ff-b0faa926a5c7.png)

R은 고객들이 영화에 메긴 평점들

S = R*R^t으로 유사도

![image-20220825171848538](https://user-images.githubusercontent.com/97595340/188319882-d440b046-0e4a-40ba-be63-891de2955b7a.png)

### 1. numpy sort

UbyU = R*R^T 해서 대각선을 0으로 만들어준 matrix(자기 자신은 이웃이 아니기 때문)

```python
# numpy의 sort
import numpy as np
a = np.array([[4,3,5,7],
            [1,12,11,9],
            [2,15,1,14]])
np.sort(a, axis=1) # axis=0이면 각각의 행을 정렬 1이면 열을 정렬
array([[3,4,5,7],[1,9,11,12],[1,2,14,15]])
```

```python
# numpy의 argsort
# 정렬된 "순서만" 알고 싶을 때 사용한다.
import numpy as np
a = np.array([[4,3,5,7],[1,12,11,9],[2,15,1,14]])
np.argsort(a axis=1)
array([[1,0,2,3],[0,3,2,1],[2,0,3,1]])
```

![image-20220825211459605](https://user-images.githubusercontent.com/97595340/188319896-313a9373-8c36-4560-8f9d-12a5360b1d33.png)

```python
import numpy as np
def predict(R,K) :
    num_users = R.shape[0]
    num_items = R.shape[1]
    
    sim = compute_sim(R)
    topk = sim.argsort(axis=1)[:,-K:] # 각 행마다 맨 뒤의 K개 element가져옴 
```

![image-20220825212433003](https://user-images.githubusercontent.com/97595340/188319912-a58aed03-f1e1-4bba-9bc1-03e871165d55.png)

### 2. 직접 predict구하는 과정.

```python
def compute_sim(R) : # 유사도 계산
    num_users = R.shape[0]
    UbyU = (R*R.transpose()).toarray()
    UbyU[range(num_users), range(num_users)] = 0
    return UbyU

def predict(R,K) : # 직접 predict행렬 산출
    num_users = R.shape[0]
    num_items = R.shape[1]
    
    sim = compute_sim(R)
    topk = sim.argsort(axis=1)[:,-K:]
    
    R_predicted = np.zeros((num_users,num_items))
    for i in range(num_users) :
        weights = sim[i, topk[i]]
        for j in range(K) :
            R_predicted[i] = weight[j] * R[topk[i,j]]
        R_predicted[i] /= weights.sum()
    
    return R_predicted
```

![image-20220825214935582](https://user-images.githubusercontent.com/97595340/188319932-4771b8cf-792a-4794-b6b7-0aadd0ad09a5.png)





