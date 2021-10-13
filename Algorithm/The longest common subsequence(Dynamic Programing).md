# The longest common subsequence(Dynamic Programing)

## Dynamic Programming

- General approach
    - 작은 문제들을 합쳐서 솔루션을 얻은후 합친다.
    - Bottom-up접근법이다.
    - 작고, 간단한걸로 시작한다.
    - subproblem의 값을 테이블에 저장한다. 그리고 나중에 사용한다.
    - 큰 솔루션을 위해 작은 솔루션을 합친다.
- 최적화 문제에 사용된다.
    - 최적화된 값을 솔루션으로 찾는다.
    - 최소화 혹은 최대화
- Divede and Conquer → 많은 중복연산이 발생한다.
Dynamic Programming → 좀더 효과적이다.
- Dynamic Programming 4 step
    - 최적화된 솔루션 구조를 특성화한다.
    - 재귀적으로 최적화된 솔루션의 값을 정의한다.
    - bottom-up으로 값을 계산한다.
    - 계산된 값으로 최적화된 결과를 도출한다.

## The longest common subsequence

### 배경

- EX) 두가지의 염색체가 얼만큼 "similarity"있는지 판단.
    - s1=ACCGGTCGAGTGCGCGGAA
    - s2=GTCGTTCGGAATGCCGTTG 일때
    - 아래 그림처럼 s1,s2의 subsequence의 공통이 길수록 높아진다.
    - 순서는 같고 연속일 필요는 없다.
    
    ![6-1](https://user-images.githubusercontent.com/76714485/137087918-0135655a-0c05-4605-a24a-3c32ae796698.png)

    

### Common Subsequence

- Subsequence 정의:
    - X=<x1,x2...xm>이면 Z=<z1,z2...zn>이면
    - Z는 X의 subsequence다.
    - 단 z의 원소는 점차적으로 증가하는 방햐잉여야한다.(순서 지켜야한다.)
    - EX) X=<A,B,D,F,M,Q>이면
          Z=<B,F,M>가능하다.
- Common Subsequence 란?→ 두 sequence의 subsequence중 공통되는 sequence다.
- **Longest Common Subsequence(LCS)**
    - LCS란?  → 두 sequence의 subsequence중 공통되는 sequence 중 가장긴 sequence
    - EX) x=heroically, y=scholarly → LCS=holly
    - Navie approach → 모든 x의 element에서 y에 있는지 체크
    →Θ(n2^m)이다. 2^m의 x의 subsequence에 n의 체크를 곱한값이다.
- **Prefix of a subsequence란?**
    - X=<x1,x2...xm>이면 Xi=<x1,x2,..,xi>
    - EX) X=<A,B,C,D,E,F,H,I,J,L>
    →X4=<A,B,C,D>, X2=<A,B>, X0=<>

### Find Longest Common Subsequence(by Dynamic Programming)

- **Optimal Substructure**
    - Z=<z1...zk>가 X,Y의 LCS라 가정한다.
    X=<x1...xm>, Y=<y1,...yn>
    - **if xm==yn이면 zk==xm==yn이므로 Z(k-1)는 Xm-1, Yn-1의 LCS다.**
        
        ![6-2](https://user-images.githubusercontent.com/76714485/137087936-3186bc16-3212-4495-85db-4b166320b220.png)

        
    - **if xm≠yn이고 zk≠xm 이면 Z는 Xm-1, Y의 LCS다.**
       
        ![6-3](https://user-images.githubusercontent.com/76714485/137087948-883e03f5-4917-4210-ac45-63f20133911d.png)

        
    - **if xm≠yn이고 zk≠yn 이면 Z는 X, Yn-1의 LCS다.**
        
        ![6-4](https://user-images.githubusercontent.com/76714485/137087957-2a388971-cf61-4615-a636-943e09bdb416.png)

        
- Optimal substructure 의 Case 경우수
    - **Case1 :** xm=yn이면 find LCS Xm-1, Yn-1
    - **Cas2 :**  xm!=yn이면
    **find** LCS Xm, Yn-1와 find Xm-1, Yn
    **Pick** 둘중 긴걸 선택해라
- Recurrence for LCS
    
    ![6-5](https://user-images.githubusercontent.com/76714485/137087971-f79770e7-2af0-4dee-8cde-7879dae129c7.png)

    
- **LCS를 Recursive로 구할시**
    
    아래와같은 구조를 이룬다. O(2^n+m)이다.
    (왼쪽가지는 Xm-1,Y을 가운데 가지는 Xm-1,Yn-1을 오른쪽 가지는 X,Yn-1을 나타낸다.)
    
    ![6-6](https://user-images.githubusercontent.com/76714485/137087988-80e2a91b-9f5f-4b0e-bf49-989bdb2065e1.png)

    
    ```python
    def lcs(X,Y,m,n):
        if m==0 or n==0:
            return 0
        elif X[m-1]==Y[n-1]:
            return 1+lcs(X,Y,m-1,n-1)
        else:
            return max(lcs(X,Y,m,n-1),lcs(X,Y,m-1,n))
    
    X="AXYT"
    Y="AYZXT"
    Z=""
    m=len(X)
    n=len(Y)
    
    print(lcs(X,Y,m,n)) #3
    ```
    
- LCS를 Comput length of optimal로 구할시.
    
    Case1 : LCS[i][j]에서X[i]와 Y[j]가 같으면 LCS[i][j]= LCS[i-1][j-1]+1이다.
    Case2 :  LCS[i][j]에서X[i]와 Y[j]가 다르면 LCS[i][j]는 max( LCS[i-1][j], LCS[i][j-1]) 이다.
    
    ![6-8](https://user-images.githubusercontent.com/76714485/137088015-6ba0e298-aa9a-430e-84df-f2a4cddcb7d7.png)

    
- LCS코드 값을 구하는코드는?
    
    ```python
    def lcs(X,Y,n,m):
        b=[[0]*(m+1) for _ in range(n+1)]
        c=[[0]*(m+1) for _ in range(n+1)]
        #b 번호 메길시 왼쪽위는 1 위에서온거 2 왼쪽에서온거 3 
        #세로줄에는 X가 가로줄에는 Y가있음. 각격자에는 LCS값
        for i in range(1,n+1):
            for j in range(1,m+1):
                if X[i-1]==Y[j-1]:
                    c[i][j]=c[i-1][j-1]+1
                    b[i][j]=0
                elif c[i-1][j]>=c[i][j-1]:
                    c[i][j]=c[i-1][j]
                    b[i][j]=2
                else:
                    c[i][j]=c[i][j-1]
                    b[i][j]=3
        return (b,c)
    
    X="spanking"
    Y="amputation"
    n=len(X)
    m=len(Y)
    
    b,c=lcs(X,Y,n,m)
    for i in c:
        print(i)
    # c
    # [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
    # [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
    # [0, 0, 0, 1, 1, 1, 1, 1, 1, 1, 1]
    # [0, 1, 1, 1, 1, 1, 2, 2, 2, 2, 2]
    # [0, 1, 1, 1, 1, 1, 2, 2, 2, 2, 3]
    # [0, 1, 1, 1, 1, 1, 2, 2, 2, 2, 3]
    # [0, 1, 1, 1, 1, 1, 2, 2, 3, 3, 3]
    # [0, 1, 1, 1, 1, 1, 2, 2, 3, 3, 4]
    # [0, 1, 1, 1, 1, 1, 2, 2, 3, 3, 4]
    ```
    
- LCS의 sequence를 구할려면?
    
    밑에그림처럼 되돌아가서 LCS가 무엇인지 구한다.
    (단 코드상은 X,Y의 자리가 위치가 반대이다.)
    b는 어디서 온지 흔적을 기록한다.
    
    ![6-9](https://user-images.githubusercontent.com/76714485/137088035-ac5ee5d8-c42f-461e-a1aa-dd41748108d1.png)

    

```python
def lcs(X,Y,n,m):
    b=[[0]*(m+1) for _ in range(n+1)]
    c=[[0]*(m+1) for _ in range(n+1)]
    #b 번호 메길시 왼쪽위는 1 위에서온거 2 왼쪽에서온거 3 
    #세로줄에는 X가 가로줄에는 Y가있음. 각격자에는 LCS값
    for i in range(1,n+1):
        for j in range(1,m+1):
            if X[i-1]==Y[j-1]:
                c[i][j]=c[i-1][j-1]+1
                b[i][j]=1
            elif c[i-1][j]>=c[i][j-1]:
                c[i][j]=c[i-1][j]
                b[i][j]=2
            else:
                c[i][j]=c[i][j-1]
                b[i][j]=3
    return (b,c,i,j)

def printLCS(b,X,i,j):
    if i==0 or j==0:
        return
    if b[i][j]==1:
        printLCS(b,X,i-1,j-1)
        print(X[i-1])
    elif  b[i][j]==2:
        printLCS(b,X,i-1,j)
    else:
        printLCS(b,X,i,j-1)

X="spanking"
Y="amputation"
n=len(X)
m=len(Y)

b,c,i,j=lcs(X,Y,n,m)

for i in b:
    print(i)
printLCS(b,X,n,m)

# [0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
# [0, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2]
# [0, 2, 2, 1, 3, 3, 3, 3, 3, 3, 3]
# [0, 1, 3, 2, 2, 2, 1, 3, 3, 3, 3]
# [0, 2, 2, 2, 2, 2, 2, 2, 2, 2, 1]
# [0, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2]
# [0, 2, 2, 2, 2, 2, 2, 2, 1, 3, 2]
# [0, 2, 2, 2, 2, 2, 2, 2, 2, 2, 1]
# [0, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2]
# p
# a
# i
# n
```

- 시간 복잡도
    - Θ(mn) → table b,c구하는데 사용
    - Θ(m+n)  → print LCS에 사용
    - 총 : Θ(mn)
