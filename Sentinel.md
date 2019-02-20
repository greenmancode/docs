# Unofficial Sentinel Beta Documentation

Created by Greenman#1559

Keep in mind:
1. This was not created by the developers of Sentinel
2. This might not be 100% accurate
3. Sentinel is still in Beta and things are subject to change

### getgenv
```lua
table getgenv()
```
Returns Sentinel's globals (_G) table.

### getrenv
```lua
table getrenv()
```
Returns Roblox's internal globals (_G) table.

### getrawmetatable
```lua
table getrawmetatable(any)
```
Returns the metatable of the passed in item without invoking `__metatable`

### getreg
```lua
table getreg()
```
Returns Roblox's registry table.

### getsenv
```lua
table getsenv(userdata script)
```
Returns the script's environment table

### setreadonly
```lua
none setreadonly(table table,boolean value)
```
Sets the read-only value of the specified table

### isreadonly
```lua
boolean isreadonly(table table)
```
Returns the read-only value of the specified table

### require
```lua
table require(userdata modulescript)
```
Returns a table with the contents of `modulescript`

### loadstring
```lua
function loadstring(string code)
```
Compiles the provided string as a Lua code (into a function).

### decompile
```lua
string decompile(userdata script)
```
Decompiles the source code of the specified `LocalScript` or `ModuleScript` as a string.

### 
