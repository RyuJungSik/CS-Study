# Knapsack Problem(Dynamic Programming)

## Knapsack Problem

### **Knapsack Problem란?**

- 배경
    - n개의 물건이 있다. <item1, item2... item n>
    - 각 item에는 wi >0, vi>0 인 무게와 값어치가 있다.
    - 배낭에는 W의 무게 제한이 있다.
    - 목표 : 배낭에 들어갈 수 있는최대 value값은?
- Navie approach → O(2^n)

### Knapsack Problem by Dynamic Programming

- **Definition**
    - OPT(i,w) → 1~i까지의 아이템중 무게제한이 w일때의 최대 value값이다.
    - **Case 1 :** OPT가 item i를 선택하지 않은 경우
        - 배낭 제한은 그대로 w이다.
    - **Case2 :** OPT가 item i를 선택한 경우
        - 배낭 제한은 새롭게 w-wi로됨
- **Recurrence for Knapsack**
    
    ![7-1](https://user-images.githubusercontent.com/76714485/137146317-b668ef6d-2fa5-4b16-9305-ac7b09e0711e.png)

    
    - **Base Case** : OPT(0,w)=0이다.
    - **Recursive step :** i 번째  아이템 선택한 경우와 선택하지 않은경우로 나눈다.
- 
    
    ![7-2](https://user-images.githubusercontent.com/76714485/137146329-7fd3afea-af79-4876-acf2-1e04898f4204.png)

    

```python
def knapscak(W,n):
    OPT=[[0]*(W+1) for _ in range(n+1)]
    for i in range(1,n+1):
        for w in range(1,W+1):
            if weight[i-1]>w:
                OPT[i][w]=OPT[i-1][w]
            else:
                OPT[i][w]=max(OPT[i-1][w], value[i-1]+OPT[i-1][w-weight[i-1]])
    return OPT

weight=[1,2,5,6,7]
value=[1,6,18,22,28]
capacity=11
n=len(weight)

OPT=knapscak(capacity,n)
for i in OPT:
    print(i)
print(OPT[n][capacity])

# result
# [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
# [0, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1]
# [0, 1, 6, 7, 7, 7, 7, 7, 7, 7, 7, 7]
# [0, 1, 6, 7, 7, 18, 19, 24, 25, 25, 25, 25]
# [0, 1, 6, 7, 7, 18, 22, 24, 28, 29, 29, 40]
# [0, 1, 6, 7, 7, 18, 22, 28, 29, 34, 35, 40]
# 40
```

- Performance
    - table 만드는데 O(nW)이다.
    - 답의 흔적 돌아가는데 O(n)든다.
