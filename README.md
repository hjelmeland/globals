This is a very simple Lua program that list reports global variable usage in Lua files, based on static analysis.

It uses 'luac', the Lua compiler, and parses the bytecode listing. No other dependencies. Works with both Lua 5.1 and 5.2.

It builds on test/global.lua in the lua-5.1.4 distribution. 

#Install
Just copy globals.lua to somewhere in your PATH and make it executable. Or use
luarocks:

	luarocks install globals-lua

#Usage
```
globals.lua <list of files to check>
```
#Example

```
$ globals.lua  test.lua 

test.lua
     _G           : 9
     arg          : 9
     io           : 9
     ipairs       : 9
     os           : 82
 !!! prev_name    : 49 50 52s
 !!! s            : 20s 21 24 26
     string       : 24 26 53
     table        : 30 35 51 62 71
     tonumber     : 30

local _G,arg,io,ipairs,os,prev_name,s,string,table,tonumber
    = _G,arg,io,ipairs,os,prev_name,s,string,table,tonumber


```

* Lines where a global is written to are marked with 's'
* Globals not preloaded in Lua is marked with  '!!!'
* Last is a list of local declarations that you can paste to the 
	top of the file in order to turn all global usages into locals. 
* Name of 'luac' can be overridden with environment variable LUAC


#See also
A much more complete tool is [luacheck](https://github.com/mpeterv/luacheck),
which also warns about unused locals. I my self use luacheck in combination with 
globals.lua.

Egil Hjelmeland, 2012; License MIT

