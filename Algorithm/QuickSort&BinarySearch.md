# QuickSort and BinarySearch(Divide-and-Conquer)

## QuickSort

- **QuickSort 3단계**
    - **Divide** : pivot x를 기준으로 2개의 subarray를 만들고 정렬한다.
        
        ![Untitled](https://user-images.githubusercontent.com/76714485/136748372-d752b12e-ea69-4654-945d-dc0db44763a4.png)

        
    - **Conquer** : 2개의 subarray를 재귀해서 sort한다.
    - **Combine** : Trivial
- 작동 방식

![Untitled 1](https://user-images.githubusercontent.com/76714485/136748432-70dbc243-f16d-4686-9dbe-85a4568dece3.png)


- **QuickSort 3단계**
    - 정렬한 배열을 A[p..r]이라 한다.
    - **Divide** : A[p...q-1], A[q+1...r]으로 나눈다.
    pivot=A[q]일때 piviot값을 기준으로 나눈다.,
    - **Conquer** : A[p...q-1], A[q+1...r] 재귀해서 sort한다.
    - **Combine** : subarray 는 이미 sort되어서 합치는데 일이 필요없다.

### **Partition**

```python
def PARTITION(A,p,r):
    x=A[r] #pivot
    i=p-1
    for j in range(p,r):
        if A[j]<=x:
            i=i+1
            A[i],A[j]=A[j],A[i]
    A[i+1],A[r]=A[r],A[i+1]
    return i+1

A=[2,8,7,1,3,5,6,4]
print(PARTITION(A,0,len(A)-1)) #3
print(A) #[2, 1, 3, 8, 7, 5, 6, 4]
```

![5-3](https://user-images.githubusercontent.com/76714485/136748454-2bab0ba7-7b9f-48fd-a063-32e0dc907d7a.png)


- **Correct of Partiton**
    - 조건
        - A[p..i]≤pivot
        - A[i+1...j-1]>pivot
        - A[r]=pivot
    - **Initiallization :** 
    loop시작전 모든 조건은 만족한다.
    왜냐하면 r=piviot이고(i=p-1) 이여서 subarray인  A[p...i], A[i+1...j-1]은 empty이다.
    - **Maintenance :**
    loop가 돌면서 
    if A[j]≤pivot 이면 A[j]와 A[i]가 swap되고 i,j가 상승ㄹ한다.
    if A[j]>pivot 이면 j만 상승한다.
    - **Termination :**
    j=r이면 loop는 끝난다.
    A[p...i]≤pivot이고 A[i+1...r-1]>pivot이다. A[r]=pivot이다.
- Θ(n) 이다.

### QuickSort

```python
def PARTITION(A,p,r):
    x=A[r] #pivot
    i=p-1
    for j in range(p,r):
        if A[j]<=x:
            i=i+1
            A[i],A[j]=A[j],A[i]
    A[i+1],A[r]=A[r],A[i+1]
    return i+1

def quickSort(A,p,r):
    if p<r:
        q=PARTITION(A,p,r)
        quickSort(A,p,q-1)
        quickSort(A,q+1,r)
    else:
        return

        
A=[2,8,7,1,3,5,6,4]
quickSort(A,0,len(A)-1)
print(A) #[1, 2, 3, 4, 5, 6, 7,
```

### Performance of QuickSort

- Running Time은 Partitioning에 달렸다.
- Subarray → balanced이면 mergeoSort보다 빠르다.
- Subarray → unbalanced이면 insertSort만큼 느리다.
- **Best Case**
    - subArra가 ≤n/2 elements일때
    - T(n)=2T(2/n)+Θ(n)
    - =Θ(nlogn)이다.
    
    ![Untitled 2](https://user-images.githubusercontent.com/76714485/136748481-8c061fbe-8758-4796-be24-1115edf8ec2e.png)

    
- **Worst Case**
    - T(n)=T(n-1)+T(0)+Θ(n)
    - =T(n-1)+**Θ(n)**
    - =Θ(n^2)
    
    ![Untitled 3](https://user-images.githubusercontent.com/76714485/136748499-ffaa69b5-9751-4614-8920-833eb44ac58e.png)


## Binary Search

- 목적 : element X를 찾은다 Sorted된 A[1...n]에서
- Navie → 1~n까지 탐색한다.
- **Binary Search(by Divde and Conquer) 3단계**
    - **Divide :** divide 2배열로 나눈다. A[1..mid], A[mid+1...n]
    - **Conquer :** 
    A[mid]=x → return mid
    A[mid]<x → select A[mid+1..n]을 다시 재귀
    A[mid]>x → select A[1..mid-1]을 다시 재귀
    - **Combine :** 결과를 return

```python
def binarySearch(A,low,high,key):
    mid=(low+high)//2
    if low==high:
        return mid
    elif mid<key:
        answer=binarySearch(A,mid+1,high,key)
    else:
        answer=binarySearch(A,low,mid-1,key)
    return answer
    
A=[1,2,3,4,6,7,9]
key=6
print(binarySearch(A,0,len(A)-1,key)) #4
```

![Untitled 4](https://user-images.githubusercontent.com/76714485/136748516-22c354da-a0e7-4a86-a5fe-3af65d8a5801.png)

- T(n)=1T(n/2)+Θ(1)
- → T(n)=Θ(logn)이다.
