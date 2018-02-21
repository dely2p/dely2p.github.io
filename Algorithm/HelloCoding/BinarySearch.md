# # Binary Search

- 선택정렬(Binary Search): 정렬된 list에서 어떤 원소를 찾을 때, 앞에서부터 하나씩 비교하며 찾는 것보다 가운데 값이랑 비교하여 찾는 원소보다 작은지 큰지를 알고 찾는 방향을 두는 것이 빠르다는 알고리즘.

https://github.com/dely2p/swift-Algorithm/blob/master/BinarySearch.playground/Contents.swift

```swift

import UIKit

// Binary Search

func run() {
    let list = [1, 3, 5, 7, 9]
    let item = 7
    let result = binarySearch(list: list, item: item)
    print(result)
}

func binarySearch(list: [Int], item: Int) -> Int {
    var low = 0
    var high = list.count-1
    while low < high {
        let middle = (low+high)/2
        let guess = list[middle]
        if guess == item {
            return guess
        }else if guess > item {
            high = middle - 1
        }else {
            low = middle + 1
        }
    }
    return 0
}

run()

```
