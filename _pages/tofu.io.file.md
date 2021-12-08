---
layout: module
category: module
namespace: tofu.io
title: file
permalink: /modules/tofu.io.file/
---
# Usage

```lua
local File = require("tofu.io.file")
```

## Functions

### File.**load**(name : string) : string

Loads the file `name` and return its content as a Lua binary-encoded string.

### File.**store**(name : string, data : string)

Stores the Lua binary-encoded string `data` into the file `name` (overwriting any existing file, in the case).

> This function saves a file into the [local user-dependent storage](/guides/virtual-file-system). Any archive mount point in use is not modified (as they are read-only in nature).
