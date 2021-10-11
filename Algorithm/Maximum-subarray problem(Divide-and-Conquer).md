# Maximum-subarray problem(Divide-and-Conquer)

## Maximum-subarray problem(Divide-and-Conquer)

- Maximum-subarray problem이란?
    - input : 크기가 N인 배열(원소에 음수 가능하다.) 
    EX) [-2,-3,4,-1,-2,1,5,-3]
    - output :  배열중 연속하는 원소의 최대합
    [-2,-3,**4,-1,-2,1,5,**-3]
- Navie한 방식으로 설계
O(n^2)
1~n-1
2~n-1
...모든 연속된 합을 구하는 방식이다.
    
    ![5-1](https://user-images.githubusercontent.com/76714485/136740247-e1709f81-8566-4633-b0a7-d4ff5599378d.png)


### Sloving by divide-and-conquer

- O(nlogn)이다.
- **Subproblem :** Find subarray A[low...high] → 초기는 low=1, high=n
- **Divide :** 사이즈가 동일한 two subarray로 나눈다. 
A[low...mid], A[mid+1...high]
- **Conquer :** A[low...mid], A[mid+1...high]에서 최대값으 subarray를 찾는다.
- **Combine :** 추가적으로 midpoint를 cross하는 subarray찾는다.
    
    ![5-2](https://user-images.githubusercontent.com/76714485/136740254-1aa9c88f-3cd4-461b-a19a-7442a03143cd.png)

    
- **cross midpoint 하는 subarray 찾는법**
    - low≤ i ≤ mid인 i에서 A[i...mid]의 최대값을 찾는다.
    - mid+1< j ≤ high인 i에서 A[mid+1...j]의 최대값을 찾는다.
    - 구하는 코드
    
    ```python
    def findMaxCrossingSubarray(A,low,mid,high):
        # left
        leftSum=-1
        sum=0
        for i in range(mid,low-1,-1):
            sum=sum+A[i]
            if sum>leftSum:
                leftSum=sum
                maxLeft=i
        
        #right
        rightSum=-1
        sum=0
        for j in range(mid+1,high+1):
            sum=sum+A[j]
            if sum>leftSum:
                rightSum=sum
                maxRight=j
    
        return [maxLeft,maxRight,leftSum+rightSum]
    
    A=[-2,-3,4,-1,-2,1,5,-3]
    print(findMaxCrossingSubarray(A,0,3,7)) #[2,6,7]
    
    #mid subarray = [4,-1,-2,1,5]
    ```
    
    - Run time : O(n)
- **Find-Maximum-Subarray**
    
    ```python
    import sys
    def findMaxCrossingSubarray(A,low,mid,high):
        # left
        leftSum=-(sys.maxsize+1)
        sum=0
        maxLeft=0
        maxRight=0
        for i in range(mid,low-1,-1):
            sum=sum+A[i]
            if sum>leftSum:
                leftSum=sum
                maxLeft=i
        
        #right
        rightSum=-(sys.maxsize+1)
        sum=0
        for j in range(mid+1,high+1):
            sum=sum+A[j]
            if sum>rightSum:
                rightSum=sum
                maxRight=j
    
        return [maxLeft,maxRight,leftSum+rightSum]
    
    def findMaximumSubarry(A,low,high):
        if high==low:
            return [low,high,A[low]]
        else:
            mid=(low+high)//2
            leftLow,leftHigh,leftSum=findMaximumSubarry(A,low,mid)
            rightLow,rightHigh,rightSum=findMaximumSubarry(A,mid+1,high)
            crossLow,crossHigh,crossSum=findMaxCrossingSubarray(A,low,mid,high)
    
            if leftSum>=rightSum>=crossSum:
                return [leftLow,leftHigh,leftSum]
            elif rightSum>=leftSum>=crossSum:
                return [rightLow,rightHigh,rightSum]
            else:
                return [crossLow,crossHigh,crossSum]
    
    A=[-2,1,-3,4,-1,2,1,-5,4]
    print(findMaximumSubarry(A,0,len(A)-1)) #[3,6,6]  -> [4,-1,2,1]
    ```
    
    ![Untitled](https://user-images.githubusercontent.com/76714485/136740270-4a9c88ed-ea2d-45c8-af50-fe1761963820.png)

    

### Analysis of Maximum-subarray

- **Base Case** : high와 low가 같은 경우 n=1이다. → T(n)=O((1)
- **Recursive Case:**
    - Dividng → Θ(1)
    - Conquering Two subproblem(n/2) → T(n)=2T(n/2)
    - Combining (FindMaxCrossingSubarray)→ Θ(n)
- T(n)=Θ(1)+2T(n/2)+Θ(n)+Θ(1)
→ T(n)=2T(n/2)+Θ(n)
- T(n)=
{Θ(1) (n=1) }
{ 2T(n/2)+Θ(n) (n>1)}
- O(nlogn)
