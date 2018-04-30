```swift
import Foundation

func solution(_ n:Int, _ words:[String]) -> [Int] {
    var connectWord: Character?
    var usedWords = [String]()
    var number = 0
    var turn = 0
    // 끝말잇기
    for (index, word) in words.enumerated() {
        if index > 1 {
            number = index % n + 1
            turn = index / n + 1
            // 끝말과 첫째말이 같은지 확인
            if word.first == connectWord! {
                // 글자 수 확인
                if word.count < 2 {
                    return [number, turn]
                }
                // 이미 말했던 글자인지 확인
                if usedWords.contains(word) {
                    return [number, turn]
                }
            } else {
                return [number, turn]
            }
        }
        usedWords.append(word)
        connectWord = word.last!
    }
    return [0, 0]
}

//print(solution(3, ["tank", "kick", "know", "wheel", "land", "dream", "mother", "robot", "tank"]))
//print(solution(5, ["hello", "observe", "effect", "take", "either", "recognize", "encourage", "ensure", "establish", "hang", "gather", "refer", "reference", "estimate", "executive"]))
print(solution(2, ["hello", "one", "even", "never", "now", "world", "draw"]))
```