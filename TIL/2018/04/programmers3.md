```swift
import Foundation

func solution(_ a:[Int], _ b:[Int]) -> Int {
    var bTeamPoint = 0
    var bPoints = b
    var minGap = -1
    var bIndexOfmin = 0
    for aValue in a {
        for (index, bValue) in bPoints.enumerated() {
            // bValue가 aValue 보다 크면 gap을 검사해보기
            if aValue < bValue {
                // min gap을 찾기
                let gap = bValue - aValue
                // 더 작은 gap이거나 처음 시작하는 gap이면 minGap 업데이트
                if minGap > gap || minGap < 0 {
                    bIndexOfmin = index
                    minGap = gap
                }
            }
        }
        // 다 돌고 나서 minGap인 값이 있다면 point +1 해주고, 그 인덱스 값은 배열에서 remove 하기
        if minGap > 0 {
            bTeamPoint += 1
            bPoints.remove(at: bIndexOfmin)
        }
        minGap = -1
    }
    return bTeamPoint
}

print(solution([5,1,3,7], [2,2,6,8]))
print(solution([2,2,2,2], [1,1,1,1]))
//print(solution([4,2,1,8], [5,9,2,1]))

```