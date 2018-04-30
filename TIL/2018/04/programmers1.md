```swift
import Foundation

func solution(_ d:[Int], _ budget:Int) -> Int {
    var countOfsupportTeam = 0
    var maxSupportTeam = 0
    //sort
    let sortD = d.sorted(by: >)
    
    // 큰 예산부터 순서대로 처리해보기
    for index in 0..<sortD.count {
        var possibleBudget = budget
        countOfsupportTeam = 0
        
        // sortD를 index부터 시작해서 끝까지
        for dIndex in index..<sortD.count {
            if possibleBudget-sortD[dIndex] < 0{
                break
            }
            possibleBudget -= sortD[dIndex]
            countOfsupportTeam += 1
        }
        if maxSupportTeam < countOfsupportTeam {
            maxSupportTeam = countOfsupportTeam
        }
    }
    return maxSupportTeam
}

print(solution([2,2,3,3], 10))

```