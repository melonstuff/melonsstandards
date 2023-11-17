[![code_logo](https://i.imgur.com/Ap07IFZ.png)](/CODE.md)

---
# Indentation Spacing, and Newlines
> All indentation should be done with 4 spaces, not a 4 width tab, 4 literal space characters.  

> No spaces after opening brackets/parens, or before closing
> ```lua
> print(123)   -- good
> print( 123 ) -- bad
> ```

> Exceptions are given to the parenthesis following an end in an anonymous function

> No spaces before opening call arguments  
> ```lua
> print () -- bad
> ```

> Spaces required after commas in call arguments only if function is not a function relating to colors
> ```lua
> print(255,0,0)   -- bad
> Color(255,0,0)   -- good
> print(255, 0, 0) -- good
> ```

> Newlines are allowed anywhere that you feel they would look best, dont act dumb.

# Naming
| Type | Rule |
| :--: | :--: |
| `local`s | `snakecase` |
| globals | `snakecase` |
| modules | `snakecase` |
| `table.Members` | `PascalCase` |
| `table:Methods` | `PascalCase` |
| `local CLASS`   | `UPPER_CASE` |
| `local PANEL`   | `UPPER_CASE` |
| `function(ar, gs)`  | `snakecase` |
| `String:Identifiers` | `Pascal:Case`|
| `ENUM_` | `UPPER_CASE` |
| `RTAndMaterialNames` | `PascalCase` |

# CStyle Syntax Usage
| Disallowed | Use Instead |
|:---:|:---:|
| `//` | `---` |
| `/**/` | `---\n---` | 
| `~=` | `!=` |
| `!` | `not` |

> The rationale behind allowing `!=` but not `!` is that `~=` is nonstandard in the whole of programming, quite simply, I'm used to typing `!=`, and I'm used to typing `not`.

> `continue` is allowed in all cases, if it works, use it.

# Bad Syntax
> `goto`'s are bad, don't use them unless they make sense semantically more than a `continue`.  

> `while` and `repeat` are bad, don't use them unless you have to. If you feel you need one, try something else.  

# Comments
> Comments should be in pairs of atleast three ticks
> ```lua
> -- bad comment
> --- good comment
> ```
> The rationale behind this is so fonts can take advantage of multidash ligatures

> Multiline comments should be avoided unless debugging  
> Always use sets of single line comments

> Four ticks should be used for obj descriptions, three for random comments

> **FOLLOW [THE DOC FORMAT](/DOCS.md)**

# Modules
> Each addon, script, program, should have one global, one module (excluding ENUMs)  

> This table should contain everything relating to the addon itself

> Configuration should not be limited the a `.config` member module, and instead should be in the root of the addon

> What constitutes a "Module" is a table that contains functions and non-constant data  

# Classes
> Classes should be defined in their own region
> ```lua
> do ---- ClassName
>   local CLASS = {}
>   CLASS.__index = CLASS
>   global_module.ClassName = CLASS
> end
> ```

> All classes should have a reference stored in your global module, as showed above

# Enumerations
> Enums can be globals but should generally be in a module
>```lua
> global_module.ENUM_A = 1
> global_module.ENUM_B = 2
> global_module.ENUM_C = 3
>
>```