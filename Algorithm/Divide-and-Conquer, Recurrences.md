# Divide-and-Conquer

## Divide-and-Conquer

- **여러개의 design paradigms이 존재한다.**
    - incremental approach(EX Inserion sort)
    - Divide-and-conquer
    - Greedy-algorightms
    - Dynamic-programming
- **Divide-and-conquer**
    - **Divide :** 문제를 여러 작은 문제로 나눈다.
    - **Conquer :** 여러 작은 문제를 recursively하게 푼다. 충분히 작으면 직접 푼다.
    - **Combine :** 작은 문제들을 ****원래 문제로 되돌아가게 합친다.
- **Divide-and-conquer(Merge Sort)**
    - **Divide :** 배열을 n/2로 나눈다.ㄴ
    - **Conquer :** 
    만약 배열의 길이가 1이면 sorted되어 있는 것이다.
    그렇지 않으면 merge sort를 재귀적으로 부른다.
    - **Combine :** 두 배열을 합친다.

## Recurrences

- recurrence는 방정식, 부등식이다.
    - 하나 또는 여러개의 base case를 갖는다.
    - 그리고 그거 스스로 작은 inputs을 갖는다.
- recurrence의 예시
    - EX1)
    T(n)=
    {1} (n=1)
    {T(n-1)+1} (n>1)
    solution → T(n)=n
    - EX2)
    T(n)=
    {1} (n=1)
    {2T(n/2)+n}(n>1)
    solution → T(n)=nlgn+n
- Divide-and-conquer의 recurrence
    
    ![3-3](https://user-images.githubusercontent.com/76714485/136391368-a2d4a32b-a836-4436-8fad-9a0f8bab6b24.png)

- Recurrence를 사용하는 이유
    - 많은 알고리즘의 복잡도를 쉽게 recurrence를 통해 표현 가능하다.
    - 많은 재귀 알고리즘의 복잡도를 쉽게 recurrence를 통해 표현 가능하다.

### Methods for Solving Recurrences

- T(n) → input이 n 일때 Merge Sort 에서 일어나는 비교 횟수
- Merge-sort recurrences
    
    ![3-4](https://user-images.githubusercontent.com/76714485/136391390-deaabb9d-2ff6-4269-b17f-686181297846.png)
    
    
- T(n)=2T(n)+n으로 표현 가능하다.
- Solution → T(n)=O(nlog2 n)
- **Proof by Recursion Tree**
    - 결과 : T(n)을 만족하면 Solution이  T(n)=O(nlog2 n) 만족한다
    - 증명
        
        ![3-5](https://user-images.githubusercontent.com/76714485/136391404-c14bd0eb-0c47-485f-95ba-f7f1d4ad898e.png)

        
- **Proof by Telescoping**
    - 결과 : T(n)을 만족하면 Solution이  T(n)=O(nlog2 n) 만족한다
    - 증명
        
        ![3-6](https://user-images.githubusercontent.com/76714485/136391413-8543a987-88fe-4bd9-97ab-ab97cfafeeb5.png)

        
    - T(n)=2T(n/2)+1 을 양변을 n으로 나누면
    T(n)/n=2T(n/2)/n+1이다.
    - T(n/2)=2T(n/4)+n/2이므로 4째줄이 가능하다.
    - 반복하면 결국 log2N이 가능하다. → 양변에 나눈 n을 다시곱하면
    - T(n)=O(nlog2 n)이다.
- **Proof by induction**
    - 결과 : T(n)을 만족하면 Solution이  T(n)=O(nlog2 n) 만족한다
    - 증명
        - Base Case : n=1 인상황
        - Inductive hypothesis : T(n)=nlog2N이 참이라 가정한다.
        - Goal : T(2n)=2nlog2(2n)이 참임을 증명하면 된다.

## The master method for solving recurrences

- master method →  solving recurrences하는데 cookbook같다
- T(n)=aT(n/b)+f(n)형태만 가능하다.
- a → number of subproblems
n/b → size of subproblem
f(n) → work dividing and combining
- a≥1, b>1, f(n) : 양의 함수
- **Master theorem (Case1)**
    - T(n)=aT(n/b)+f(n) (a≥1, b>1)
        
        ![3-7](https://user-images.githubusercontent.com/76714485/136391428-c82a5785-0117-4ed7-959a-debcb1b30686.png)

        
    - 이 가능하다.
    - EX) a=9, b=3이면 O(n^2)
- **Master theorem (Case2)**
    - T(n)=aT(n/b)+f(n) (a≥1, b>1)
        
        ![3-8](https://user-images.githubusercontent.com/76714485/136391440-3a84f1a1-924d-45df-826e-8d3824359e28.png)

        
    - 이 가능하다.
- **Master theorem (Case3)**
    - T(n)=aT(n/b)+f(n) (a≥1, b>1)
    - f(n)이 다음을 만족하고
        
        ![3-9](https://user-images.githubusercontent.com/76714485/136391454-558c1fcf-4ad6-4005-ac95-d550e7d0e66e.png)

        
    - 상수 c<1과 모든 충분히 큰 n에대해서 다음을 만족하면
        
        ![3-10](https://user-images.githubusercontent.com/76714485/136391466-da850575-55d0-4d04-8283-da10fe839638.png)

        
    - 라 할 수 있다.
        
        ![3-11](https://user-images.githubusercontent.com/76714485/136391480-d0f1c930-8940-4897-acdc-19323b39466b.png)
