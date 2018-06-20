# 문장

###- 지역변수
: local을 붙여서 지역변수로 사용할 수 있다.

```lua
local var = 10
```
  
    
    

###- 제어구조
: if ~ than ~ end 형식으로 쓸 수 있다. lua는 {} 없이 쓰는 syntax를 가지고 있기 때문에 다음과 같이 쓸 수 있다.   

(elseif를 붙여서 쓰는 것은 오타가 아님 주의!)

```lua
if val == 1 then
	print("val==1")
elseif val == 2 then
	print("val==2")
elseif val == 3 then
	print("val==3")
else
	print("else")
end
```


  
   
###- break, return문
: lua에서도 break문으로 조건문이나 반복문을 빠져나올 수 있고, return으로 함수에서 값을 return 시킬 수 있다.
(return 관련 예제는 다음 장인 function에서 나올 예정)
 