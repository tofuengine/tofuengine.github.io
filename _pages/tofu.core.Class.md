---
layout: default
category: module
namespace: tofu.core
title: Class
permalink: /modules/tofu.core/Class/
---
# tofu.core.Class

```lua
local Class = require("tofu.core").Class
```

---

## Functions

### Class.**define**(model = nil)

Defines a new class, by optionally implementing `model` interface. The newly defined class will have a
variable-arguments static method `new(...)` that will optionally class the `__ctor(..)` method to initialize the
instance.

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

### Class.**implement**(proto, model)

### Class.**dump**(table)
