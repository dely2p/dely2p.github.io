# Question 02.

> 문제

피보나치 배열은 0과 1로 시작하며, 다음 피보나치 수는 바로 앞의 두 피보나치 수의 합이 된다. 정수 N이 주어지면, N보다 작은 모든 짝수 피보나치 수의 합을 구하여라.

예제)

Input: N = 12
Output: 10 // 0, 1, 2, 3, 5, 8 중 짝수인 2 + 8 = 10.
    
    
> 풀기

```swift
func fibonacci(N: Int) -> Int{
    var arr = [0, 1]
    var index = 1
    var result = 0
    while arr[index] < N {
        // 피보나치 수열 만들기
        arr.append(arr[index-1] + arr[index])
        
        // 만약 짝수면 더하기
        if arr[index] % 2 == 0 {
            result += arr[index]
        }
        index += 1
    }
    return result
}

print(fibonacci(N: 12))
```