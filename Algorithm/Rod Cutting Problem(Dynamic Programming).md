# Rod Cutting Problem(Dynamic Programming)

## Rod Cutting Problem

### Rod Cutting Problem이란?

- 긴 n inches 길이인 rod가 있다.
- pi → 는 i(길이)에 따른 가격이다.
- rn → 은 자른 횟수를 말한다.
- 목적 : 몇번을 잘라야 최대의 price를 얻을 수 있는지 구하시오.
- EX) 위와같은 rod=4가 주어지고 table에선 2 2로 자를떄가 이득이 10으로 최대이다.
    
    ![7-3](https://user-images.githubusercontent.com/76714485/137890437-88ed0485-bb38-49c5-ab94-5533e090e56a.png)

- **Naive approach**
    - 2^(n-1) 방법이 존재한다.
        
        ![7-4](https://user-images.githubusercontent.com/76714485/137890463-3f2ef776-67fe-4b0b-8f6c-3a1d5eef0043.png)

        
    - 모든 경우를 구할 수 있다.

### Optimal solution

- rn 은 길이 n에서의 최대 이득값이다.
- pn은 자르지 않고 얻는 이득값이다.
- 길이가 n이면 최대 이득값은
    - → max(pn, r1+rn-1, r2+rn-2 ... rn-1+r1)이다.
- **Optimal Substructure**
    - 사이즈 n인 문제를 작은 subprombles으로 만든다.
    - 자른뒤 2개의 subproblem이 있다. → 그 둘은 각각 독립된 rod-cutting문제이다.
    - 작은 subproblem에서 optimal solution.을 구해 합친다.

### Recursive Solution

- **Recursive Structure**
    - 자르지 않은 pn을 남겨둔다.
    - 그후 max(pi+rn-i) (1≤i≤n)
    - 두 값을 비교한다.
        
        ![7-5](https://user-images.githubusercontent.com/76714485/137890472-9ca26bfa-aade-47d0-8dfb-98199e5a062c.png)

        
- 코드

```python
def cutRod(p,n):
	if n==0:
		return 0
	q=-10000000000
	for i in range(1,n+1):
		q=max(q,p[i]+cutRod(p,n-1))
	return q
```

- 트리로 보면 다음과 같다.
    - 매우 비효율적이다.
    
    ![7-6](https://user-images.githubusercontent.com/76714485/137890497-ba1ed6ed-d4b8-4bc9-a8d9-c486ef068e0b.png)

    
- **Recurrence**
    
    ![7-7](https://user-images.githubusercontent.com/76714485/137890504-45cb4196-c0e6-47c9-8908-b115c7192520.png)

    
    - solution : T(n)=2^n이다.

### Dynamic Solution

- 같은 subproblem을 반복하지 않고 한번만 구한다.
- subproblem의 테이블을 저장한다.
- subproblem을 사이즈로 sort한후 작은거 부터 푼다.

```python
def bottomUpCutRod(p,n):
    r=[i for i in range(n+1)]
    for j in range(n):
        q=-10000000
        for i in range(1,j):
            q=max(q,p[i]+r[j-i])
        r[j]=q
    return r[n]
```

- O(n^2)이다
- 구성요소 찾는법 추가시.
    
    ```python
    def bottomUpCutRod(p,n):
        r=[i for i in range(n+1)]
    		s=[i for i in range(1,n+1)]
        for j in range(n):
            q=-10000000
            for i in range(1,j):
                if q<p[i]+r[j-i]:
    							q=p[i]+r[j-i]
    							s[j]=i
            r[j]=q
        return (r,s)
    
    def prtinCutRodSolution(p,n):
    	while n>0:
    		print(s[n]
    		n=n-s[n]
    ```
    
    ![7-8](https://user-images.githubusercontent.com/76714485/137890594-52641853-9325-4bbd-b2ed-0fc0c4721ff8.png)

    
    
    
