---
layout: default
category: module
namespace: tofu.core
title: Log
permalink: /modules/tofu.core/Log/
---
# Usage

```lua
local Log = require("tofu.core").Log
```

## Rationale

## Functions

### Log.**info**(...)

Dump the function arguments to console, with `INFO` severity level. Each argument is automatically converted
to string by (implicitly) calling the `tostring()` function.

### Log.**warning**(...)

Dump the function arguments to console, with `WARNING` severity level. Each argument is automatically converted
to string by (implicitly) calling the `tostring()` function.

### Log.**error**(...)

Dump the function arguments to console, with `ERROR` severity level. Each argument is automatically converted
to string by (implicitly) calling the `tostring()` function.

### Log.**fatal**(...)

Dump the function arguments to console, with `FATAL` severity level. Each argument is automatically converted
to string by (implicitly) calling the `tostring()` function.
