# OLD Cyber Documentation
Created by Greenman#1559. This is not official documentation.

Last Updated: Nov. 10 2018

Update: 
This documentation is now old and is here for archival purposes.

~~[Inspiration](https://targaryentech.com/api.html)~~
The website isn't there anymore. I just copied from the Visenya (roblox exploit) API documentation.

~~[Cyber CW Thread](https://v3rmillion.net/showthread.php?tid=783281)~~
Update: Thread deleted so I will include my synopsis here.
Cyber started out as a shitty wrapper that costed $10 made by Pudding Mug. Shortly after release, it's exposed for being skidded off of Axon. Jumping forward to "Cyber V3", this is when I bought the exploit (I was stupid lol). I don't know why but I was dickriding the exploit and was on the support team so I wrote these docs. The working Cyber I had was one of the most unstable and incomplete wrappers I've ever used. In the end, it turned out that Cyber was skidding off of ScriptWare.

### getrenv

Returns a table populated with the main Roblox thread environment
```lua
Table<Variant> getrenv(<None> nil)
```

### getgenv

Returns a table populated with the main Cyber thread environment
```lua
Table<Variant> getgenv(<None> nil)
```

### getrawmetatable

Returns the metatable of passed object without invoking the __metatable metamethod
```lua
Table<Variant> getrawmetatable(Variant<Object> obj)
```

### setrawmetatable

Sets an object's metatable without invoking __metatable metamethod.

```lua
Table<Variant> setrawmetatable(Variant<Object> obj, Table<Variant>)
```

### setreadonly
Sets the read-only property of 'table' according to the boolean 'val'
```lua
None setreadonly(Table table, Boolean val)
```

### isreadonly

Returns the readonly value of specified table
```lua
Boolean isreadonly(Table table)
```

### loadstring
Attempts to compile a function with the specified script
```lua
Variant<Function, (Nil, String)> loadstring(String src, String chunkName="@CyberChunk")
```

### dofile
Attempts to compile and run a script given a file path. Will return nil and string error if exception occurs
```lua
Variant dofile(String path)
```

### setclipboard
Copy specified data to clipboard
```lua
None setclipboard(String data)
```

### loadfile
This function no longer exists

### writefile
Attempts to write data to file
```lua
None writefile(String fileName, String data)
```

### debug.getupvalue 
Returns the value of the specified upvalue at the index
```lua
Variant getupvalue(Variant<Function undefined, int> index, String upvalueName)
```

### debug.setupvalue
Returns true if the upvalue at the specified index was found, and set. False otherwise.
```lua
Boolean setupvalue(Variant<Function undefined, int> idx, String upvalueName, Variant value)
```

### printconsole
Outputs a string to the Cyber console
```lua
None printconsole(String text)
```

### hideconsole
Hides the Cyber console
```lua
None hideconsole(<None> nil)
```

### showconsole
Makes the Cyber console reappear after using `hideconsole`
```lua
None showconsole(<None> nil)
```

### getglobal
The standard Lua C [lua_getglobal](https://pgl.yoyo.org/luai/i/lua_getglobal) function
```lua
None getglobal (String globalname)
```

### getfield
The standard Lua C [lua_getfield](https://pgl.yoyo.org/luai/i/lua_getfield) function
```lua
None getfield(Variant<int> idx, String fieldname)
```

### pushstring
The standard Lua C [lua_pushstring](https://pgl.yoyo.org/luai/i/lua_pushstring) function
```lua
None pushstring(String string)
```

### pushnumber
The standard Lua C [lua_pushnumber](https://pgl.yoyo.org/luai/i/lua_pushnumber) function
```lua
None pushnumber(Variant<int> n)
```

# Events
### MouseButton1Click
### MouseButton2Click
### MouseButton3Click
### MouseButton1Up
### MouseButton1Down
### MouseButton2Up
### MouseButton2Down
### MouseButton3Up
### MouseButton3Down
