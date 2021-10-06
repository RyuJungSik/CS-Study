# Merge Sort

## Merge Sort

- Divided-and-conquer approach을 사용한다.
- recursion 컵셉이 기반이다.
- **Divide-and-conquer**
    - **Divide :** 문제를 여러 작은 문제로 나눈다.
    - **Conquer :** 여러 작은 문제를 recursively하게 푼다. 충분히 작으면 직접 푼다.
    - **Combine :** 작은 문제들을 ****원래 문제로 되돌아가게 합친다.
- **Divide-and-conquer(Merge sort 적용)**
    - **Divide :** 원소 n개의 배열을 n/2 배열로 각각 나눈다.
    - **Conquer :** merge-sort를 재귀적으로 호출하여서 sub배열을 sort한다.
    만약 길이가 1이면 직접 solve한다.
    - **Combine :** 정렬된 2개의 sub배열을 합쳐 sort된 합쳐진 배열을 갖는다.
- Combine 에선 Merge 알고리즘을 사용한다.
- merge-sort 코드
    
    ```python
    def mergesort(l):
    	if len(l)<2:
    		return l
    	mind=len(l) //2
    	left=mergesort(l[:mid])
    	right=mergesort(l[mid:])
    	return merge(left,right)
    ```
    
    - n=1이면 done
    - 절반을 기준으로 left, right으로 재귀한다.
    - **Merge 함수를 통해 두 배열을 합친다.**

### Merge 과정

- 
    
    ![3-1](https://user-images.githubusercontent.com/76714485/136224862-41ec3942-fbd3-4572-b136-571d89b5379b.png)

- Left : p~q이고 Right : q+1 ~ r이다.(q=(p+2)/2)
- 각각의 sub배열은 정렬된 상태이다.
- INF를 통해 끝값을 표시한다.
- 두 배열의 두개의 값을 비교해서 각각 작은값을 넣어준다.
- n번만에 합치기 가능하다.
- Merge 함수

### Merge 함수 분석


![3-2](https://user-images.githubusercontent.com/76714485/136224828-d104caa1-f5a0-41ac-abbf-e73cffa2ab1d.png)


- 12 ~ 17 줄이 어떻게 Merge가 되는지 보이는 곳이다.
Loop invariant가 필요하다.
- 첫 loop시 A[p...k-1]이고 Left와 Right의 k-p째 작은 수를 포함한다.
- L[i], R[j]는 각 배열에 가장 작은 원소값을 갖는다.
- **Prove Merge Correct algorithm (loop invariant)**
    - **Initialization** :
        - 첫 loop 시 k=p이다
        - 이말은 A배열인 A[p..k-1]은비어있다.
        - k-p=0이므로 A는 0번째 작은 값이다.
        - i=j=1이므로 L[i], R[j]는 가장 작은 요소를 가르킨다.
    - **Maintenance :**
        - loop 들어가면 A[p..k-1]는 k-p번째 작은 값(L,R에서의)들이 들어 있다.
        - 만약 L[i] ≤ R[j]이면
        L[i]는 A에 복사되지않은 가장 작은값이다.
        line 14에서 A[k]로 복사된다.
        그러면 A[p...k]는 k-p+1 번째 작은 값을 갖는다.
        k, i 값을 증가시킨다.
        - 만약 L[i] ≥ R[j]이면
        위와 동일한 프로세스를 돌아간다.
    - **Termination :**
        - A[p...k]는 k-p+1 번째 작은 값을 갖는다.(정렬된 L,R에서.)
        - k=r+1로 반복문을 빠져나왔을때  A[p...k]는 A[p..r](전체배열)이다.
        - L,R은 n1+n2+2(2는 INF 2개) 원소를 갖는다.
        - n1+n2=(r-p)+1이다. 즉 모든 원소가 배열안에 들어가 있다.
