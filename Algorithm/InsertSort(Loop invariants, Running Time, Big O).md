# Sorting Problem

## Sorting Problem

- input : sequence <a1, a2,...an> of numbers [2,5,3,6]
- output : permutation <a'1,a'2...a'n> 단 a'1≤a'2≤...a'n [2,3,5,6]
- pseudocode:
    
    ![Untitled](https://user-images.githubusercontent.com/76714485/136055785-c0fce6c5-fc0e-4463-8eec-c0c113b1c45d.png)

    ![1-1](https://user-images.githubusercontent.com/76714485/136055832-a85ca841-1f99-466a-91f8-0fe0bfe5d8a2.png)

    
- for 문은 2번째  오른쪽으로 증가
- while문은 왼쪽으로 작은수 만날때까지 자리를 옮긴다.
- 파이썬 코드로 구현

```python
def insertSort(A):
    n=len(A)
    for j in range(1,n):
        key=A[j]
        i=j-1
        while i>=0 and A[i]>key:
            A[i+1]=A[i]
            i=i-1
        A[i+1]=key
    return A

A=[8,2,4,9,3,6]
print(insertSort(A)) #[2, 3, 4, 6, 8, 9]
```

## Loop invariants

- 위의 Insert-sort를 수도코드상
    - 밖의 루프는 j-1까지의 sort된 정렬된것을 보장한다
    - 그 결과 모든 루프를 다 돌면 sub array A[1...j-1]은 원래 배열과 동일해지고 sort된 상태이다.
- Loop invariant은  3가지를 보여야 한다.
    1. **Initialization :** 선행하는 첫번째 루프가 참이여야한다.
    2. **Maintenance :** 만약 이전 반복이 참이면 다음반복도 참이여야한다.(j→j+1)
    3. **Termination** : 루프가 끝날때, invariant가 유용한 정보를 주고, 그정보를 통해 알고리즘참을 증명해야한다.

### Insert-Sort loop invariant

![Untitled](https://user-images.githubusercontent.com/76714485/136055785-c0fce6c5-fc0e-4463-8eec-c0c113b1c45d.png)

- **Initialization**
    - 1개의 원소가 있을때 정렬된 상태이기 때문에 첫 루프에서 참이다.
    - j 는 항상 2로 시작하므로 size는 항상 1이므로 정렬된 상태 맞다.
- **Maintenance**
    - 만약 현재 루프에서 배열이 sort 되어 있다면 다음 배열도 정렬된 상태인가? 맞다
    - inner loop를 보면, inner loop에서 나오면 j가 자기 자리를 찾아간다.
    - outer loop를 돌때마다 A[1...j-1]은 정렬된다.
- **Termination**
    - loop가 끝나면 sort되어 있나? 맞다.
    - j=n+1일때 loop가 종료되며, j=n일때 배열은 sort되어 있다.
    - 그러므로, loop종료시 배열 정렬되어잇는거 맞다.

## Running time

- 어떤 알고리즘이 i 라인이면 각각 상수 시간이 걸린다. RAM에서 처리할때.
- 각줄을 c1, c2, c3...으로 표현 가능하다.
- 만약 loop가 없을시 → c1+c2....+ci로 표현 가능하다. 상수다.
- loop가 있으면
    - input값에 따라 달라진다.
        - 이미 정렬된 배열은 더쉽다.
        - 배열 사이즈에 따라 다르다.
        - 일반적으로 upper bound를 찾는다. → 모든사람이 보장되기 때문에.
    - 상수값이아니게 된다.

![Untitled](https://user-images.githubusercontent.com/76714485/136055785-c0fce6c5-fc0e-4463-8eec-c0c113b1c45d.png)

- 위의 표를보면
    - cost → 컴퓨터가 읽는데 걸리는 시간
    - times → 특정라인이 반복되는 수
    - t.j → j에 따라 while이 진행하는 수
- total cost → 각 라인은 cost * times
    
    ![1-2](https://user-images.githubusercontent.com/76714485/136055920-baec62d5-217a-45ec-8dfa-697873c1a602.png)

    
- Best Case → [1,2,3,4,5]와 같이 이미 정렬된 상황
    - 6,7라인의 times는 0이된다.
    - 위의 T(n)을 정리하면
    - T(n)=An-B(A,B constant) → O(n)이다.
- Worst Case → [5,4,3,2,1]와 같은 경우
    - tj→j와 동급이고 그결과
    - line 5 시그마를 풀면→ n(n+1)/2-1이고
    - line 6,7은  시그마를 풀면 → (n-1)n/2이다
    - T(n)=An^2+Bn+C(A,B,C constant) → O(n^2)이다.
    
- Kinds of analyses
    - Worst-case:(usually)→ T(n)=maximum time of 알고리즘
    - Average-Case:(sometimes) → 확률이 필요하다.
    - Best-Case:특정한 상황에서만 작동한다.

## Big O

- Asymptotic Notation
    - an^2+bn+c → 간단히 n^2으로 나타낸다.
- 보통 O를 주로 쓴다.
- all the runnig-time cost → f(n) 이라할때
- 만약 f(n)=cn(log n)+cn일때
- 우린 running time 알고리즘을 다른 함수로 표현하고자한다.
- f(n)=O(g(n))으로 표현가능하다.
- O(g(n))={양의 상수 c>0, n0≥0에서 0≤f(n)≤cg(n)을 (n≥n0에서) 만족한다.}
- 즉,  f(n)=O(g(n))은 g(n)은 upper bound on f(n)이라 할 수 있다.

### f(n) ∈ O(g(n)) 증명

- 항상 정해진 양식 적용
- EX1) f(n)=7n-1이고 g(n)=n일때,  f(n)∈O(g(n))을 증명하라.
    1. f(n)≤c*g(n)을 만족하는 (n≥n0에서) c>0, n0≥0이 존재한다. 
    2. choose c=7, n0=1이라 할때
    f(n)=7n-1
          ≤7n (n≥1)
          ≤c*n
          ≤c*g(n)이다
    3. 위의 식을 통해 f(n)≥c*g(n)은 n≥n0인 모든 n에서 만족한다.
    4. 따라서 f(n)∈ O(g(n))이다.
- EX2)  f(n)=n^3+100n^2이고 g(n)=n^3일때,  f(n)∈O(g(n))을 증명하라.
    1. f(n)≤c*g(n)을 만족하는 (n≥n0에서) c>0, n0≥0이 존재한다.
    2. choose c=101, n0=0이라 할때
    f(n)=n^3+100n^2
          ≤**n^3+100n^3 (n≥0)**  **→ 이부분이 c,n0처리 증명 부분이다.**
          =101n^3
          =c*n^3
          =c*g(n)이다
    3. 위의 식을 통해 f(n)≤c*g(n)은 n≥n0인 모든 n에서 만족한다.
    4. 따라서 f(n)∈ O(g(n))이다.
- EX3)  f(n)=n^3+100n^2이고 g(n)=n일때,  g(n)∈O(f(n))을 증명하라.  아까와는 반대이다.
    1. g(n)≥c*f(n)을 만족하는 (n≥n0에서) c>0, n0≥0이 존재한다.
    2. choose c=1, n0=0이라 할때
    g(n)=n^3
          ≤**n^3+100n^2 (n≥0)**
          =1(n^3+100n^2)
          =c(n^3+100n^2)
          =c*f(n)이다
    3. 위의 식을 통해 g(n)≤c*f(n)은 n≥n0인 모든 n에서 만족한다.
    4. 따라서 g(n)∈ O(f(n))이다.

### insert sort의 big O

- worst 경우만 O(n^2)이다.
- insert sort의 running time은 input의 특성에 따라 달라진다.
- 즉, 모든 inser sort는 O(n^2) under을 보장한다.

## Practice Test

<details>
<summary>Practice Test</summary>
      
### 문제1

![t1-1](https://user-images.githubusercontent.com/76714485/136055961-0bb3fff9-821b-45bb-b015-854e1a7d9032.png)


### 해설1

![a1](https://user-images.githubusercontent.com/76714485/136055979-d07583e1-a541-4465-9a1d-d370da7ef538.png)


![a2](https://user-images.githubusercontent.com/76714485/136055990-8850f5ac-add9-4ea8-866e-d666ab990176.png)


![a3](https://user-images.githubusercontent.com/76714485/136056009-53eca311-d713-4513-84cd-e87fb2bb3e45.png)


![a4](https://user-images.githubusercontent.com/76714485/136056023-b6e64426-1ec9-4176-838c-9466f53baefb.png)


### 문제2

![t1-2](https://user-images.githubusercontent.com/76714485/136056042-72f2fb6c-b720-4514-b8d8-59836074aede.png)


### 해설2

- EX2-1)  f(n)=2n^3+10n^2이고 g(n)=3n^3일때,  f(n)∈O(g(n))을 증명하라.
    1. f(n)≤c*g(n)을 만족하는 (n≥n0에서) c>0, n0≥0이 존재한다.
    2. choose c=1, n0=10이라 할때
    f(n)=2n^3+10n^2
          ≤3n^3 **(n≥10)**  **→ 그래프를 이용하여 증명가능**
          =1*3n^3
          =c*3n^3
          =c*g(n)이다
    3. 위의 식을 통해 f(n)≤c*g(n)은 n≥n0인 모든 n에서 만족한다.
    4. 따라서 f(n)∈ O(g(n))이다.
- EX2-2)  f(n)=2n^3+10n^2이고 g(n)=3n^3일때,,  g(n)∈O(f(n))을 증명하라.  아까와는 반대이다.
    1. g(n)≥c*f(n)을 만족하는 (n≥n0에서) c>0, n0≥0이 존재한다.
    2. choose c=2, n0=0이라 할때
    g(n)=3n^3
          ≤4**n^3+20n^2 (n≥0) → 그래프를 이용하여 증명가능**
          =2(2n^3+10n^2)
          =c(2n^3+10n^2)
          =c*f(n)이다
    3. 위의 식을 통해 g(n)≤c*f(n)은 n≥n0인 구간에서 모든 n에서 만족한다.
    4. 따라서 g(n)∈ O(f(n))이다.
    
    궁금증 : 증명법 그래프 가능한지.
    

### 문제3

![t1-3](https://user-images.githubusercontent.com/76714485/136056084-cf587a40-6ba1-45d2-bbf7-d990d3a36a2c.png)



### 해설

- (1)
    
    ![a-3-1](https://user-images.githubusercontent.com/76714485/136056327-8da2acf1-edea-4656-9a9f-3f7b62fbb777.png)

    
- (2)
    
    ![a-3-2-2](https://user-images.githubusercontent.com/76714485/136057532-c3a24203-191a-455f-861c-fa68cf56b7c0.PNG)


    
- 
    
    ```python
    def min_max_lin(L):
        min=L[0]
        max=L[0]
        for e in L:
            if max<e:
                max=e
            if min>e:
                min=e
        return (min,max)
    
    L=[2,3,7,1]
    print(min_max_lin(L)) #(1,7)
    ```

</details>


