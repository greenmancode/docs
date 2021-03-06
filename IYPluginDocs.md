# Infinite Yield Plugin Documentation
<hr>

[Infinite Yield Discord](https://discord.io/infiniteyield)

[Infinite Yield Website](https://infyield.yolasite.com/)

Infinite Yield is developed by Edge#2928, Zwolf#3762, and Moon#0653

Documentation written by Greenman#8153

Additional IY Function Docs (click [here](https://luatsuki.github.io/site/index.html)) made by ZWolf

Last Update: Friday, 02-Aug-2019 13:49:03

<hr>

# Contents
* [Creating A Plugin](#creating-a-plugin)
* [Adding Commands To A Plugin](#adding-commands-to-a-plugin)
* [Infinite Yield's Core Functions](#infinite-yield-core-functions)
    * [getstring](#getstring)
    * [getPlayer](#getplayer)
    * [notify](#notify)
    * [randomString](#randomstring)
    * [splitString](#splitstring)
    * [Time](#time)
    * [FindInTable](#findintable)
    * [GetInTable](#getintable)
* [Loading Plugins](#loading-plugins)

<hr>


Infinite Yield plugins are a way for you to add custom content to your command list. You can share this content or keep it to yourself without worrying about editing Infinite Yield every time we release an update.

Plugins are `.iy` files and should be placed in the `workspace` folder of your exploit.

## Creating A Plugin
First of all, open your favorite Lua editor. (Examples: Notepad++, ZeroBrane Studio, Visual Studio Code)

Start by setting up a module that returns a table. I recommend that you name the table Plugin
```lua
local Plugin = {
}

return Plugin
```

Now you need to set up the properties of the plugin and the commands table by adding keys to your `Plugin` table.

The following is the basic keys used to set plugin properties:

`string PluginName` : The name of your plugin. Keep in mind that your filename must match the value of this property.

`string PluginDescription` : The description of your plugin. If the plugin name is self-explanatory, use this as the credits.

`table Commands` : A table where all of your commands will be created

Here is a template to guide you:

```lua
local Plugin = {
    ["PluginName"] = "NAME HERE",
    ["PluginDescription"] = "DESCRIPTION HERE",
    ["Commands"] = {
    }
}

return Plugin
```

## Adding Commands To A Plugin

Once you have a plugin setup, you are ready to start adding commands in the `Commands` table. Each command is a key in the table that is usually named the command.

Here is the keys for each command:

`string ListName` : This is where you put your command (along with arguments in square brackets). You can show the user and aliases here too.

`string Description` : The message you want to appear when the user clicks the command in the list for more information.

`table Aliases` : This is the aliases that you can use to run the command. Make sure that the table is sorted and each element of the table is an alias for your command. If you don't want to create any aliases for your command, leave this table empty.

`function Function` : This is the function that is executed when the user runs your command.

Arguments: 
1. `table args` : A table containing the arguments passed into the command
2. [Player](https://developer.roblox.com/api-reference/class/Player) `speaker` : The user's player object (game.Players.LocalPlayer)

Note: Infinite Yield contains global functions that you can use in commands. This will be covered in another section.

Each command should follow this format:
```lua
--Note: This is just a snippet
["EXACTCOMMAND"] = {
    ["ListName"] = "COMMAND [ARGUMENT]",
    ["Description"] = "DESCRIPTION HERE",
    ["Aliases"] = {"ALIAS1","ALIAS2","ALIAS3"},
    ["Function"] = function(args,speaker)
        --CODE
    end
}
```


Here is an example:
```lua
local Plugin = {
    ["PluginName"] = "ExamplePlugin",
    ["PluginDescription"] = "This is a helpful template",
    ["Commands"] = {
        ["print"] = {
            ["ListName"] = "print [text]",
            ["Description"] = "Outputs text to the Roblox console",
            ["Aliases"] = {"p","out","output"},
            ["Function"] = function(args,speaker)
              print(getstring(1))  
            end
        },
        ["notify"] = {
            ["ListName"] = "notify [text]",
            ["Description"] = "uses the notification function",
            ["Aliases"] = {'alert'},
            ["Function"] = function(args,speaker)
                notify('Notification Title',getstring(1))
            end
        }
    }
}

return Plugin
```

If you are struggling, feel free to use my template:
```lua
local Plugin = {
    ["PluginName"] = "NAME HERE",
    ["PluginDescription"] = "DESCRIPTION HERE",
    ["Commands"] = {
        ["COMMANDNAME"] = {
            ["ListName"] = "COMMANDNAME [ARGUMENT1]",
            ["Description"] = "DESCRIPTION HERE",
            ["Aliases"] = {"ALIAS1","ALIAS2","ALIAS3"},
            ["Function"] = function(args,speaker)
              --CODE HERE  
            end
        }
     }
}

return Plugin
```

## Infinite Yield Core Functions
Infinite Yield's core functions can be used in your commands. Keep in mind that these are not all of the core functions and you can find more by looking inside Infinite Yield's source code.

### getstring
```lua
string getstring((number) argument index)
```
This function is used to combine the arguments after a certain index into one string. This is useful when you have a string argument that might include spaces. 

Tip: Always make an argument that contains spaces your last argument

Example:
```lua
--Note: This is just a snippet
["Function"] = function(args,speaker)
  print(args[1])  
end
```
If we do this, every space will indicate a separate argument.

Example:

User Input: `print Hello World!`
The command will only get "Hello" because Infinite Yield sees the space and thinks "World!" is a separate argument. 

```lua
--Note: This is just a snippet
["Function"] = function(args,speaker)
  print(getstring(1))  
end
```

If we do this, we get the full message.

Example:
User Input: `print Hello World!`
The command will get "Hello World!" because it takes all the arguments after argument 1 and concatenates it to argument 1.

### getPlayer
```lua
table getPlayer((string) player name, (Player) speaker)
```
This is used to correct shorthand names to full player names. It can also be used to make names like `me`, `others`, `all`work.

Example:

Target Player: `mrcoolkid123`
User Input: `mrcool`
IY Correction: `mrcoolkid123`

The first argument should be args[index]. The index should be the index that contains the player name. For the second argument you can just pass in `speaker` (it's an argument in the function for the command).

Example:

```lua
--Note: This is just a snippet
--Command: printname [plr]
["Function"] = function(args,speaker)
  local players = getPlayer(args[1], speaker)  
end
```

Remember that `getPlayer()` will return a table so you want to use a *for pairs loop* to run code for all of the returned players.

Example:
```lua
--Note: This is just a snippet
--Command: printname [plr]
["Function"] = function(args,speaker)
  local players = getPlayer(args[1], speaker) 
  for k,v in pairs(players) do
    local Player = Players[v]
    print(Player.name)
  end 
end
```

If you are wondering where the global `Players` is from, you can find it defined inside IY's source code:

(Line 4): `Players = game:GetService("Players")`

This is not the best way to write this and is to make it simple for beginners. If you want to do this with less code, you can do it like this:

```lua
--Note: This is just a snippet
--Command: printname [plr]
["Function"] = function(args,speaker) 
  for k,v in pairs(getPlayer(args[1], speaker)) do
    print(Players[v].Name)
  end 
end
```
Now you can make your player argument work like it does with normal IY commands!

### notify
```lua
nothing notify([(string) title], (string) message)
```
The notify function is used to make an Infinite Yield message box appear. 

Example: https://vgy.me/NsSwPu.png

The first argument is the notification title (in the image it's "Notification Title"). If you don't specify this argument, the default title is "Notification Title".

The second argument is the notification text (in the image it's "Hi").

Let's see this in a plugin:
```lua
--Note: This is just a snippet
--Command: printusername
["Function"] = function(args,speaker) 
  notify("Username",speaker.Name) 
end
```

This is a great alternative to using game.StarterGui:SetCore() to make notifications.

### randomString
```lua
string randomString()
```
Generates a random string with a length of 10-19 characters.

### splitString
```lua
table splitString((string) string, (string) separator/deliminator)
```
Splits a string by a deliminator. The results are stored in the returned table.

Example Usage:
```lua
--Note: This is just a snippet
--Command: getRGBcolor
--User Input: getRGBColor 255,0,100
["Function"] = function(args,speaker) 
  local colors = splitString(args[1],",")
  local r = colors[1] --255
  local g = colors[2] --0
  local b = colors[3] --100
end
```

### Time
```lua
string Time()
```
Returns the current time as the following string: `Hour:Minute:Second AM/PM`

### FindInTable
```lua
boolean FindInTable((table) table, (any) value)
```
Checks if a value exists in a table. Returns true if the value is found and false if the value is not found.

### GetInTable
```lua
any GetInTable((table) table, (any) value)
```
Returns the index of a value in a table. Returns the index if the value is found and false if the value is not found.
Keep in mind that this function only works with **sorted tables**.

**Update:** ZWolf has documented a lot more of the core functions. Click [here](https://luatsuki.github.io/site/index.html) to see more of the core functions.

## Loading Plugins

Once you finish creating your own plugin, you are ready to use it in Infinite Yield!

Tip: You can find or post plugins in the **#plugins** channel of the Infinite Yield Discord

The first thing you need to do is to make sure that your filename is `PluginName` and that it has a `.iy` extension. Next, put your file into the `workspace` folder of your exploit.

Tip: If you are unable to see the extension of files, click the **View** tab at the top of the file explorer and check the box next to **File name extensions** ([Image Guide](https://vgy.me/ohxGWG.png))

Once you've done that, you need to load the plugin in Infinite Yield. 

1. Hover your mouse over **Infinite Yield FE** to open it up. ([Image Guide](https://vgy.me/PTEzl7.png))
2. Click the cog in the top right corner of the GUI to pull up the settings. ([Image Guide](https://vgy.me/YaJktz.png))
3. Next to **Plugins** click the **Edit** button. ([Image Guide](https://vgy.me/JnWTow.png))
4. Click the **Add** button to open the Add Plugins window. ([Image Guide](https://vgy.me/E8r9Wq.png))
5. In the text box type in the name of your plugin file (make sure not to type .iy) and click **Add Plugin**. If you did it correctly, you will get a notification box that shows your plugin name and description. ([Image Guide](https://vgy.me/eWHi6B.png))
6. Click X on the **Add Plugins** window, **Close** then the cog in Infinite Yield ([Image Guide](https://vgy.me/B755pb.png))

Now you should be able to use the commands you made in your plugin!
