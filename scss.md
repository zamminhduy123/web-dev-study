# Compiling

Browser can not understand scss language, so we have to compile it into css

> use gulp & gulp-scss

# Features
- variables
- nested rules
- using math by **import sass:math**
- map object
- has if/else, loop (@each & @for), 
- parent selector (**&**)

### mixin

it's like a **function** that is an css object, we can pass in param
- param can have default value
- if no param was pass. use `@include [mixin_name]`


### function

- we can create variables inside function
use `@return` to return value
 
# @use/@forward instead of @import
Issues: https://sass-lang.com/documentation/at-rules/import

`@use` makes it like import in javascript, it doesn't make css globally

> use `as *` if u don't want to add prefix file name to variables

Or use _index.scss to `@forward` all the things in the file
-> again it's like index file in js