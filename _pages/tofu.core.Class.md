---
layout: default
category: module
namespace: tofu.core
title: Class
permalink: /modules/tofu.core/Class/
---
# Usage

```lua
local Class = require("tofu.core").Class
```

## Description

As you might know, Lua is not an out-of-the-box object oriented programming language. It is, however, *multi-paradigm* in nature and with some clever usage of [metatables](https://www.lua.org/pil/13.html), classes can be implemented fairly easy. **Tofu Engine** offers this facility with the `tofu.core.Class` module, so that you won't need to include a [full-fledge OOP library](https://github.com/kikito/middleclass) in each and every project.

## Functions

### Class.**define**()

Defines a new class. The newly defined class will have a variable-arguments static method `new(...)` that will optionally class the `__ctor(..)` method to initialize the instance.

```lua
local Counter = Class.define()

local function Counter:__ctor(...)
  self.value = 0
end

local function Counter:increment()
  self.value = self.value + 1
end

return Counter
```

### Class.**borrow**(proto, model, criteria = nil)

Copies all the references from `model` to `proto`, much like as the concept of [mixin](https://en.wikipedia.org/wiki/Mixin), to *borrow* the functionalities.

`proto` can be either a class or an instance. In the first case, borrowed functions will be shared dynamically among every class instance. In the latter, the functions will be present only on the selected instance.

`model` can either any table (not necessarily a class created with `Class.define(...)`).

`criteria` is an optional argument specifying the behaviour when a `model` function with the same identifier is already present in class `proto`. If set to `extend` the existing function is called **before** the new one; if set to `chain` the existing function is called **after** the new one; if set to `replace` the existing function is replaced with the new one.

Any other variable (i.e. not of `function` type) present in `model` is ignored.

```lua
local A = Class.define()
function A:say()
  print("Hello from A!")
end

local B = Class.define()
function B:say()
  print("Hello from B!")
end

local C = Class.define()
function C:say()
  print("Hello from C!")
end

local c1 = C.new()
local c2 = C.new()

Class.borrow(C, B, "extend") -- Every instance of `C` will include `B` functions (appended).

Class.borrow(c2, A, "chain") -- Only instance `c2` will include `A` functions (prepended).

print("--- c1 ---")
c1:say()

print("--- c2 ---")
c2:say()
```

The example above will result in

```txt
--- c1 ---
Hello from C!
Hello from B!
--- c2 ---
Hello from A!
Hello from C!
Hello from B!
```

### Class.**dump**(table)

This is mostly a *debug* function that pretty-prints and dumps a table content to console.
