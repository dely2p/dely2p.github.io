# 함수

- Lua에서의 함수는 일반적인 프로그래밍 언어에서의 함수와 유사하다.  

1. 매개변수 값이 없는 함수 일 때

	```lua
	function printDescription()
		print("Hello Lua")
	end
	
	print(printDescription()) -- Hello Lua
	```
	
	

2. 매개변수 값이 있는 함수 일 때

	```lua
	function printInputValue(inputValue)
		print(inputValue)
	end
	
	print(printInputValue("Lua")) -- Lua
	```
	
	

3. 매개변수 값이 있고 return 값이 하나 일 때

	```lua
	function printReturnString(inputValue)
		result = "Lua "..inputValue
		return result	
	
	print(printReturnString("Hello")) -- Lua Hello
	```
	
	
	
4. 매개변수 값이 없고 return 값이 하나 이상일 때

	```lua
	function multiReturnString()
		a = "가"
		b = "나"
		c = "다"
		return a, b, c
	end
	
	a, b, c, d = multiReturnString()
	print(a, b, c, d) -- 가 나 다 nil
	```

 