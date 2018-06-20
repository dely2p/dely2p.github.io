# 반복문

###- while ~ do ~ end

```lua
val = 1
while val < 3 do
	print(val)
	val = valu + 1
end

print("end: "..val)
--[[
1
2
end: 3
]]
```


###- Repeat ~ until 조건

```lua
val = 1
repeat
	print(val)
	val = val + 1
until val == 3

print("end: "..val)
--[[
1
2
end: 3
]]
```

###- for 초기값, 종료값, 증감값 do ~ end

```lua
for index=1, 10, 2 do
	print(index)
end
--[[
1,
3,
5,
7,
9
]]
```

###- for in pairs ~ do ~ end

```lua
monster = {"피카츄", "라이츄", "파이리", pocket = 6}

for key, value in pairs(monster) do
	print(key, value)
end
--[[
1 피카츄
2 라이츄
3 파이리
pocket 6
]]
```

###- for in ipairs ~ do ~ end 

```lua
monster = {"피카츄", "라이츄", "파이리", pocket = 6, "꼬부기"}

for key, value in ipairs(monster) do
	print(key, value)
end
--[[
1 피카츄
2 라이츄
3 파이리
4 꼬부기
]]
```