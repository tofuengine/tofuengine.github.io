---
layout: default
category: module
namespace: tofu.core
title: Math
permalink: /modules/tofu.core/Math/
---
# Usage

```lua
local Math = require("tofu.core").Math
```

## Constants

### Math.**SINCOS_PERIOD**

### Math.**EPSILON**

`__FLT_EPSILON__`

## Functions

### Math.**lerp**(v0, v1, t)

### Math.**invlerp**(v0, v1, v)

### Math.**clamp**(x, lower, upper)

### Math.**step**(edge, x)

### Math.**smoothstep**(edge0, edge1, x)

### Math.**smootherstep**(edge0, edge1, x)

### Math.**sign**(x)

### Math.**signum**(x)

### Math.**sincos**(rotation) -> sin, cor

### Math.**angle_to_rotation**(angle) -> rotation

### Math.**rotation_to_angle**(rotation) -> angle

### Math.**wave**(name) -> function(t)

### Math.**wave**(name, period, amplitude = 1.0) -> function(t)

### Math.**tweener**(name) -> function(time)

### Math.**tweener**(name, duration) -> function(time)

### Math.**tweener**(name, duration, from, to) -> function(time)
