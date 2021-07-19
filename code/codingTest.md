# Codility



# Lesson1 : iterations

## 1.[BinaryGap](https://app.codility.com/demo/results/trainingHXZCHR-EYB/#)

Easy

Find longest sequence of zeros in binary representation of an integer.

### Task description

A *binary gap* within a positive integer N is any maximal sequence of consecutive zeros that is surrounded by ones at both ends in the binary representation of N.

For example, number 9 has binary representation `1001` and contains a binary gap of length 2. The number 529 has binary representation `1000010001` and contains two binary gaps: one of length 4 and one of length 3. The number 20 has binary representation `10100` and contains one binary gap of length 1. The number 15 has binary representation `1111` and has no binary gaps. The number 32 has binary representation `100000` and has no binary gaps.

Write a function:

> ```
> def solution(N)
> ```

that, given a positive integer N, returns the length of its longest binary gap. The function should return 0 if N doesn't contain a binary gap.

For example, given N = 1041 the function should return 5, because N has binary representation `10000010001` and so its longest binary gap is of length 5. Given N = 32 the function should return 0, because N has binary representation '100000' and thus no binary gaps.

Write an ***\*efficient\**** algorithm for the following assumptions:

> - N is an integer within the range [1..2,147,483,647].



### Solution

```python
# you can write to stdout for debugging purposes, e.g.
# print("this is a debug message")

# 내 풀이
def solution(N):
    # write your code in Python 3.6

    # split으로 문제 해결
    binary = bin(N)[2:] #bin(N) : 0b1001 -> 1001
    # print(binary)
    max_size = 0 # 사이즈 변수

    # '1'로 split 하기
    # ex) ['', 00, '']
    splited_binary = binary.split('1') # 1로 split

    # 2보다 작은 경우 1이 닫혀있지 않음10000, 0
    if len(splited_binary) <= 2 :
        return 0
    # 남은 리스트 중 가장 길이가 큰 0 찾기
    else :
        # 마지막이 0인 것은 1로 안닫혀있음 버림
        if '0' in splited_binary[-1] :
            splited_binary = splited_binary[:-1]
        for index, value in enumerate(splited_binary) :
            if len(value) >= max_size :
                max_size = len(value)

    return max_size



# 다른사람 풀이
def solution(N) :
    # write your code in Python 3.6

    # split으로 문제 해결
    binary = bin(N)[2:] #bin(N) : 0b1001 -> 1001
    one_index_list = []

    # 1이 있는 인덱스 모두 추가
    for index, value in enumerate(binary) :
        if value == '1' :
            one_index_list.append(index)

    bin_idx_list = []
    #  답힌 경우 아닐 때
    if len(one_index_list) <= 1 :
        return 0
    # 1과 다음 1 까지의 거리 계산으로 해결
    else :
        bin_idx_list.append(0)
        for cur_idx in range(len(one_index_list)-1) :
            bin_idx_list.append(one_index_list[cur_idx+1]-one_index_list[cur_idx]-1)

    return max(bin_idx_list)
```





# Lesson2 : Arrays

## 1. [CyclicRotation](https://app.codility.com/programmers/lessons/2-arrays/cyclic_rotation/)

### Task description

An array A consisting of N integers is given. Rotation of the array means that each element is shifted right by one index, and the last element of the array is moved to the first place. For example, the rotation of array A = [3, 8, 9, 7, 6] is [6, 3, 8, 9, 7] (elements are shifted right by one index and 6 is moved to the first place).

The goal is to rotate array A K times; that is, each element of A will be shifted to the right K times.

Write a function:

> ```
> def solution(A, K)
> ```

that, given an array A consisting of N integers and an integer K, returns the array A rotated K times.

For example, given

```
    A = [3, 8, 9, 7, 6]    K = 3
```

the function should return [9, 7, 6, 3, 8]. Three rotations were made:

```
    [3, 8, 9, 7, 6] -> [6, 3, 8, 9, 7]
    [6, 3, 8, 9, 7] -> [7, 6, 3, 8, 9]
    [7, 6, 3, 8, 9] -> [9, 7, 6, 3, 8]
```

For another example, given

```
    A = [0, 0, 0]    K = 1
```

the function should return [0, 0, 0]

Given

```
    A = [1, 2, 3, 4]    K = 4
```

the function should return [1, 2, 3, 4]

Assume that:

> - N and K are integers within the range [0..100];
> - each element of array A is an integer within the range [−1,000..1,000].

In your solution, focus on ***\*correctness\****. The performance of your solution will not be the focus of the assessment.



### Solution

`문제 풀이시 80점 받았었음, A=[] 일때, K=0일때의 조건 생각 안하고 진행했음`

```python
# you can write to stdout for debugging purposes, e.g.
# print("this is a debug message")

def solution(A, K):
    # write your code in Python 3.6
    # A : N개의 integer를 갖는 Array
    # Roation of th array : 하나의 인덱스 증가, 마지막 것은 첫번째로 이동
    # K : Rotation 횟수
    # N과 K는 0 ~ 100까지 가짐

    # 풀이?
    # 하나씩 옮기는것은 오래 걸릴 듯
    # 나눠지면 자기 자신 그대로임
    # 나머지를 이용하여 계산

    # N = 0, A=[] 일때
    if len(A) == 0 :
        return []
    # K 횟수 0번 일 때
    if K == 0 :
        return A
    if K % len(A) == 0 :
        return A
    else :
        # K횟수를 A의 길이로 나눈 나머지 만큼 이동 됨
        mod = K % len(A)
        # print(mod)
        # print(A[:-mod])
        # print(A[-mod:])
        result = []
        result.extend(A[-mod:])
        result.extend(A[:-mod])
        return result
```





## 2. [OddOccurrencesInArray](https://app.codility.com/demo/results/training4HFEKU-WAV/#)

Find value that occurs in odd number of elements.

### Task description

A non-empty array A consisting of N integers is given. The array contains an odd number of elements, and each element of the array can be paired with another element that has the same value, except for one element that is left unpaired.

For example, in array A such that:

```
  A[0] = 9  A[1] = 3  A[2] = 9  A[3] = 3  A[4] = 9  A[5] = 7  A[6] = 9
```

> - the elements at indexes 0 and 2 have value 9,
> - the elements at indexes 1 and 3 have value 3,
> - the elements at indexes 4 and 6 have value 9,
> - the element at index 5 has value 7 and is unpaired.

Write a function:

> ```
> def solution(A)
> ```

that, given an array A consisting of N integers fulfilling the above conditions, returns the value of the unpaired element.

For example, given array A such that:

```
  A[0] = 9  A[1] = 3  A[2] = 9  A[3] = 3  A[4] = 9  A[5] = 7  A[6] = 9
```

the function should return 7, as explained in the example above.

Write an ***\*efficient\**** algorithm for the following assumptions:

> - N is an odd integer within the range [1..1,000,000];
> - each element of array A is an integer within the range [1..1,000,000,000];
> - all but one of the values in A occur an even number of times.



### Solution

```python
# you can write to stdout for debugging purposes, e.g.
# print("this is a debug message")
import collections

def solution(A):
    # write your code in Python 3.6

    # A = [N integers] Not empty len(A)>=1
    # A에 odd 짝을 지어주는 숫자를 가지며, unpair 작없는 것도 존재

    # A의 길이 N은 1~10000000까지의 홀수개를 가짐
    # A는 1~1000000000 까지의 숫자를 가짐
    # A의 값중 한개를 제외한 모든 것은 짝수번 일어남
    count_A = collections.Counter(A)
    print(count_A.items())
    if len(count_A.items()) == 1 :
        return A[0]

    for key, value in count_A.items() :
        if value % 2 != 0 :
            return key

```





# Lesson3 : Time Complexity

## 1.[FrogJmp](https://app.codility.com/demo/results/trainingBQKEB6-4ZZ/#)



### Task description

A small frog wants to get to the other side of the road. The frog is currently located at position X and wants to get to a position greater than or equal to Y. The small frog always jumps a fixed distance, D.

Count the minimal number of jumps that the small frog must perform to reach its target.

Write a function:

> ```
> def solution(X, Y, D)
> ```

that, given three integers X, Y and D, returns the minimal number of jumps from position X to a position equal to or greater than Y.

For example, given:

```
  X = 10  Y = 85  D = 30
```

the function should return 3, because the frog will be positioned as follows:

> - after the first jump, at position 10 + 30 = 40
> - after the second jump, at position 10 + 30 + 30 = 70
> - after the third jump, at position 10 + 30 + 30 + 30 = 100

Write an ***\*efficient\**** algorithm for the following assumptions:

> - X, Y and D are integers within the range [1..1,000,000,000];
> - X ≤ Y.



### Solution

```python
# you can write to stdout for debugging purposes, e.g.
# print("this is a debug message")

def solution(X, Y, D):
    # write your code in Python 3.6
    # X : 개구리의 현재 위치
    # Y : 개구리가 원하는 위치
    # D : 개구리의 점프력
    # Return : 개구리는 몇 회 이상 점프해야 Y를 넘는가?

    # X <= Y
    # X,Y 1 ~ 1,000,000,000

    # 남은 거리 = 목표위치(Y) - 현재위치(X)
    distance = Y - X
    div, mod = divmod(distance, D) # 몫, 나머지
    
    # 1) 나머지가 0일 때 나누어 떨어 짐 : return 몫
    if mod == 0 :
        return div
    # 2) 몫으로 안나눠질 때 return 몫 + 1
    else :
        div += 1
        return div
```



## 2.[PermMissingElem](https://app.codility.com/demo/results/trainingYCZ348-2K5/#)

Find the missing element in a given permutation.

### Task description

An array A consisting of N different integers is given. The array contains integers in the range [1..(N + 1)], which means that exactly one element is missing.

Your goal is to find that missing element.

Write a function:

> ```
> def solution(A)
> ```

that, given an array A, returns the value of the missing element.

For example, given array A such that:

```
  A[0] = 2  A[1] = 3  A[2] = 1  A[3] = 5
```

the function should return 4, as it is the missing element.

Write an ***\*efficient\**** algorithm for the following assumptions:

> - N is an integer within the range [0..100,000];
> - the elements of A are all distinct;
> - each element of array A is an integer within the range [1..(N + 1)].



### Solution1 : 50점

```python
# you can write to stdout for debugging purposes, e.g.
# print("this is a debug message")

# 풀이1 : 50점
def solution(A):
    # write your code in Python 3.6

    # A = [N개의 다른 integer]
    # A 는 1 ~ N+1개의 integer가지는데 한개만 missing value 존재한다
    # return : missing value 값은?

    # 조건
    # N : 0 ~ 100,000
    # A 의 integer는 distinct 값 임 중복없음
    
    # sorting 후 맨앞 + 맨뒤 빼가면서 더함?
    # [1, 2, 3, 4, 5, 6, 8] # 맨 앞 맨 뒤는 더한게 최대값임 왜냐하면 중간에만 값이 부족해야 알아차릴 수 있음
    # [8, 6, 5, 4, 3, 2, 1]

    # [1, 2, 4, 5, 6, 7, 8]
    # [8, 7, 6, 5, 4, 2, 1]

    left_index = 0
    right_index = len(A)-1
    A.sort()
    B = A
    B.sort(reverse=True)

    C = A + B
    value = C[0]
    # print("value", value)

    for index in range(0, len(C)):
        # 앞 뒤 더한게 value와 다를 때
        if value != C[index] :
            # value가 클 땐 B 리스트에서 앞 뒤 비교
            # A에서 찾기            
            if value < C[index] :
                if A[index-1] != A[index]-1 :
                    return A[index]-1
            # B에서 찾기
            else :
                if B[index-1] != B[index]+1 :
                    return B[index]+1
```

### Solution 2 : 100

```python
# 풀이 2
def solution(A):

    if len(A) == 0 :
        return 1
    else :
        # [1, 2, 4, 5, 6, 7, 8]
        # 무조건 하나가 부족하며 length는 6이되 맨 마지막 숫자가 8임
        # length + 2
        totalSum = sum(range(1,len(A)+2))# 무조건 1부터 시작 함
        AListSum = sum(A) # 
        return totalSum - AListSum # 기존에 있어야할 값 - A리스트 전체 값 = 부족한 값
```

### Other Solution : 100

```python
# 다른사람 풀이
def solution(A):

    N = len(A) + 1
    S = N*(N+1)/2
    s = sum(A)

    return int(S-s)
```





## 3.[TapeEquilibrium](https://app.codility.com/demo/results/trainingECAP4P-52X/#)

Minimize the value |(A[0] + ... + A[P-1]) - (A[P] + ... + A[N-1])|.

### Task description

A non-empty array A consisting of N integers is given. Array A represents numbers on a tape.

Any integer P, such that 0 < P < N, splits this tape into two non-empty parts: A[0], A[1], ..., A[P − 1] and A[P], A[P + 1], ..., A[N − 1].

The *difference* between the two parts is the value of: |(A[0] + A[1] + ... + A[P − 1]) − (A[P] + A[P + 1] + ... + A[N − 1])|

In other words, it is the absolute difference between the sum of the first part and the sum of the second part.

For example, consider array A such that:

```
  A[0] = 3  A[1] = 1  A[2] = 2  A[3] = 4  A[4] = 3
```

We can split this tape in four places:

> - P = 1, difference = |3 − 10| = 7
> - P = 2, difference = |4 − 9| = 5
> - P = 3, difference = |6 − 7| = 1
> - P = 4, difference = |10 − 3| = 7

Write a function:

> ```
> def solution(A)
> ```

that, given a non-empty array A of N integers, returns the minimal difference that can be achieved.

For example, given:

```
  A[0] = 3  A[1] = 1  A[2] = 2  A[3] = 4  A[4] = 3
```

the function should return 1, as explained above.

Write an ***\*efficient\**** algorithm for the following assumptions:

> - N is an integer within the range [2..100,000];
> - each element of array A is an integer within the range [−1,000..1,000].



### Solution

```python
# you can write to stdout for debugging purposes, e.g.
# print("this is a debug message")

def solution(A):
    # write your code in Python 3.6

    # A : 빈 Array가 아닌 N개의 integer를 가진 array이며 테이프를 나타냄
    # P : 숫자인데 0보다 크고 N개의 Array숫자보다 작은 integer
    #     P를 통해 테이프를 2개로 나누고 빈 부분은 없다
    # Tape : 첫번째 테이프 부분(1~P), 두번째 테이프 부분(P ~ N)
    # return : 절대값, sum(tape 첫번째) - sum(tape 두번째)

    diff_list = []
    # A = [1,2,3,4,5,6]
    # 1) index = 0
    # first_tape = [1] 
    # second_tape = [2,3,4,5,6]
    # 2) index =1
    # first_tape = [1,2]
    # second_tape = [3,4,5,6]
    for idx in range(len(A)-1) :
        # print(A[:idx+1], A[idx+1:])
        # Output:
        # [1] [2, 3, 4, 5, 6]
        # [1, 2] [3, 4, 5, 6]
        # [1, 2, 3] [4, 5, 6]
        # [1, 2, 3, 4] [5, 6]
        # [1, 2, 3, 4, 5] [6]
        fist_tape = sum(A[:idx+1])
        second_tape = sum(A[idx+1:])
        diff_value = abs(fist_tape - second_tape)
        diff_list.append(diff_value)
    result = min(diff_list)
    return result
```



