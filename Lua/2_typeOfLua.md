# Lua의 타입

>###8가지 기본 데이터 타입  
####: nil, boolean, number, string, userdata, function, thread, table이 있다. 
 
###- nil
: 보통 유용한 값이 없음을 나타내기 위해 nil을 사용

###- boolean
: false, true 값을 가짐. (false, nil만 거짓, true, "", 다른 언어에서 false를 나타내는 `0`도 참)

###- number
: integer과 double형을 나타냄

###- string
: 일반적인 프로그래밍 언어에서 문자열을 나타낸다. 다만 문자열 안의 문자를 직접 변경할 수 없고 새로 문자열을 만들어 낸다.

###- userdata
: c에서 사용하는 데이터를 저장하기 위해 만들어짐(raw memory)  
종류에는 두가지-(full userdata, light userdata)가 있다. C-API에서 다룰 예정

###- function
: Lua와 C로 작성된 함수들을 모두 사용한다.

###- thread
: Lua의 쓰레드는 운영체제에 의존적이지 않음. 코루틴을 지원한다고 하는데 구체적인 내용은 코루틴에서 다룰 예정

###- table
: Lua의 테이블은 유일한 자료구조 매커니즘이다. 일반적인 배열, 리스트, 심볼테이블, sets, records, 그래프, 트리 등등을 나타낼 수 있다.  
그리고 a.x와 a["x"]는 Lua에서 같은 표현이기 때문에 둘 다 자유롭게 쓸 수 있다.