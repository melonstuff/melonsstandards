[![doc_logo](https://i.imgur.com/OTZhori.png)](/DOCS.md)

[<b><p align="center">SEE SNIPPETS.JSON</p></b>](/snippets.json)

---

# Basic Syntax
> Using the Doc Format is simple, although sometimes tedious  
> The format does **NOT** perform **ANY** complex syntax analysis, it can infer some things, but you should always be explicit

> All documentation is in comments above an object  

> `---@` is the prefix for a block command, these define what the
> current block should actually be documenting

> `----` is the prefix for a doc comment, these need to be paired with
> atleast one block command, as seen below

> `arg`, `return` and `accessor` for things are documented with a `(name: type)` pair
> 

> You may link to another object with `[add]`, this is qualifed so you can do `[module.add]`, `[module.submodule.add]`, ect, this also works with classes, everything

> Types are any class in the basegame, Lua `type()` result, or `any`  
> Types can be suffixed with `?` to indicate its optional, eg. `(a: number?)`
> Varargs are documented with `...type` if applicable, otherwise just `...`
  
> Enums are documented in types by stating `ENUM_`, eg. `NOTIFY_`
>

> Spacing between name and type in `(name: type)` should match up between lines, for example
> ```lua
> ---@arg (a:               b) Desc
> ---@arg (longname: longtype) Desc
> ```

> Small example
> ```lua
> ----
> ---@name add
> ----
> ---@arg    (a:   number) The left hand side to add
> ---@arg    (b:   number) The right hand side to add
> ---@return (apb: number) A and B added
> ----
> ---- Adds the arguments a and b together
> ----
> function add(a, b) return a + b end
> ``` 

# What gets documented?
> - Modules
> - Panels
> - Classes
> - Functions
> - Enumerations
> - Methods
> - Hooks
> - Console Commands

# Documenting Modules
> Although modules may be redefined in multiple files (ie. `x = x or {}`)
> you only need to document them once, in the most sensible file

> You must call `@module`  
> You must provide a `@realm` call with either `CLIENT`, `SERVER` or `SHARED`

> ```lua
> ----
> ---@module
> ---@name abc.def
> ---@realm CLIENT
> ----
> ---- This is a submodule inside abc
> ----
> abc.def = abc.def or {}
> ```

# Documenting Panels
> You must register the panel into your global module, as it is used for method documenting, as shown below  

> You must provide an `@panel` call with the `vgui.Register`'ed name of the Panel

> You can use the `@accessor` command here

> ```lua
> ----
> ---@panel YourPanel:Name:Here
> ---@name abc.def.yourpanelnamehere
> ----
> ---@accessor (off: bool) Is this panel off?
> ----
> ---- A demo panel
> ----
> local PANEL = vgui.Register("YourPanel:Name:Here", {}, "Panel")
> AccessorFunc(PANEL, "off", "off", FORCE_BOOL)
>
> abc.def.yourpanelnamehere = PANEL
> ```

# Documenting Classes
> Classes are documented similarly to PANELs, they follow the same rules
  
> You must call `@class` with your CLASSNAME

> You can use the `@accessor` command here

> ```lua
> ----
> ---@class CLASSNAME
> ---@name abc.def.yourclasshere
> ----
> ---@accessor (Enabled: bool) is this class enabled?
> ----
> ---- A demo class
> ----
> local CLASSNAME = {}
> CLASSNAME.__index = CLASSNAME
> abc.def.yourclasshere = CLASSNAME
> 
> AccessorFunc(CLASSNAME, "Enabled", "Enabled", FORCE_BOOL)
> ```

# Documenting Functions
> Reminder, You do not document functions the same way as methods

> You do not need to document local functions  
> Argument names do not need to match `@arg` calls names

> You can use the `@return` command here

> ```lua
> ----
> ---@name abc.def
> ----
> ---@arg    (a:   any) Input argument 
> ---@return (ret: any) Return
> ----
> ---- Does something with a value and returns it
> ----
> function abc.def(a)
>     return a
> end
> ```

# Documenting Enumerations
> Enums are documented using a special command called `@enum`

> Enums must provide an `@enumeration` call  
> Enum prefixes are defined in the `@name` call, and is assumed to be `_` concatenated  
> Enums do not require a value to be given, but do require a name in parens

> ```lua
> ----
> ---@enumeration
> ---@name NOTIFY
> ----
> ---@enum (GENERIC: 0) A generic notification
> ---@enum (ERROR:   1) An error notification
> ---@enum (UNDO:    2) An undo notification
> ---@enum (HINT      ) A hint notification
> ---@enum (CLEANUP   ) A cleanup notification
> ----
> ---- Example using the wikis NOTIFY enum
> ----
> NOTIFY_GENERIC = 0
> NOTIFY_ERROR = 1
> NOTIFY_UNDO = 2
> NOTIFY_HINT = 3
> NOTIFY_CLEANUP = 4
> ```

# Documenting Methods
> Methods are documented similarly to functions, however they are specified with the `@method` command

> Note that were using `:` in the `@name` call, you can use `.` if you want, mostly for legacy reasons

> ```lua
> ----
> ---@method
> ---@name SOMEOBJ:MethodName
> ----
> ---@arg    (a: any) In
> ---@return (b: any) Out
> ----
> ---- A random method on SOMEOBJ
> ----
> function SOMEOBJ:MethodName(a)
>     return a
> end
> ```

# Documenting Hooks
> Hooks are documented above `hook.Run`, very similarly to functions  
> Wildcard hooks eg. `Frame:LoadPage:PAGENAME` are indicated with `*`, as in `Frame:LoadPage:*`

> Hooks require a `@hook` call

```lua
----
---@hook 
---@name Frame:LoadPage:*
----
---@arg    (num: number) A random number
---@return (valid: bool) Is this number valid
----
---- Example hook documentation
----
hook.Run("Frame:LoadPage:Hello", math.random(-100, 100))
```

# Documenting Console Commands
> Console commands are documented above their `console.Add` declaration very similarly to functions

> Concommands require `@concommand`  
> Concommands cannot contain `@return` calls

```lua
----
---@concommand
---@name melon_add
----
---@arg (a: number) LHS
---@arg (b: number) RHS
----
---- Adds two numbers together
----
concommand.Add("melon_add", function(_, _, args)
    print(tonumber(args[1]) + tonumber(args[2]))
end )
```