---
layout: module
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

### Math.**SINCOS_PERIOD** : integer

When dealing with rotations (this is particularly true when dealing with [graphics](/modules/tofu.graphics/Canvas)) they aren't expressed in radians. This is due to the fact that, being radians expressed in a floating point number, it is very difficult (or, better, pretty much impossible) to ensure a properly aligned rotations (e.g. 90° degrees). To solved this, discrete (integer) degrees are used. However, instead of the usual 360 steps, a finer amount of steps are used, and the `Math.SINCOS_PERIOD` constants holds this value (which is equal to `512` as a default).

```lua
print(Math.SINCOS_PERIOD) -- `512`
```

### Math.**EPSILON** : number

This constants holds the value of `__FLT_EPSILON__`, which is used by the `Math.is_almost_zero()` and `Math.is_almost_equal()` to compare two non-integer numbers.

```lua
print(Math.EPSILON) -- `1.192093e-07`
```

## Functions

### Math.**is_almost_zero**(v : number) : boolean

Returns `true` is the number `v` *approximately* zero.

Floating point imprecision makes comparing numbers using the `==` operator inaccurate. `Math.is_almost_zero()` returns `true` if the number is within a small value (`Math.EPSILON`) from `0`.

```lua
print(Math.is_almost_zero(1.0)) -- `false`
print(Math.is_almost_zero(0.1)) -- `false`
print(Math.is_almost_zero(0.01)) -- `false`
print(Math.is_almost_zero(0.001)) -- `false`
print(Math.is_almost_zero(0.0001)) -- `false`
print(Math.is_almost_zero(0.00001)) -- `false`
print(Math.is_almost_zero(0.000001)) -- `false`
print(Math.is_almost_zero(0.0000001)) -- `true`
```

### Math.**is_almost_equal**(v0 : number, v1 : number) : boolean

Compares `v0` with `v1` and returns `true` they are *approximately* equal.

Floating point imprecision makes comparing numbers using the `==` operator inaccurate. `Math.is_almost_equal()` compares two numbers and returns `true` if they are within a small value (`Math.EPSILON`) from each other.

```lua
print(Math.is_almost_equal(1.0, 2.0)) -- `false`
print(Math.is_almost_equal(0.1, 0.2)) -- `false`
print(Math.is_almost_equal(0.01, 0.02)) -- `false`
print(Math.is_almost_equal(0.001, 0.002)) -- `false`
print(Math.is_almost_equal(0.0001, 0.0002)) -- `false`
print(Math.is_almost_equal(0.00001, 0.00002)) -- `false`
print(Math.is_almost_equal(0.000001, 0.000002)) -- `false`
print(Math.is_almost_equal(0.0000001, 0.0000002)) -- `true`
```

### Math.**lerp**(v0 : number, v1 : number, t : number) : number

Calculates the linear interpolation between values `v0` and `v1`, but a factor `t`.

The value `t` is not clamped in the range `[0, 1]`.

```lua
print(Math.lerp(1, 1000, 0.25)) -- `250.75`
```

### Math.**invlerp**(v0 : number, v1 : number, v : number) : number

Calculates the value required to produce the linearly interpolated value `v` within the range `[v0, v1]` 

The value `v` is not clamped in the range `[v0, v1]`.

```lua
print(Math.invlerp(1, 1000, Math.lerp(1, 1000, 0.25))) -- `0.25`
```

### Math.**clamp**(x : number) : number

Returns `x` clamped (i.e. limited) to the range `[0, 1]`.

```lua
print(Math.clamp(-1.0)) -- `0.0`
print(Math.clamp(0.5)) -- `0.5`
print(Math.clamp(1.0)) -- `1.0`
print(Math.clamp(999.9)) -- `1.0`
```

### Math.**clamp**(x : number, lower : number, upper : number) : number

Returns `x` clamped (i.e. limited) to the range `[lower, upper]`.

```lua
print(Math.clamp(0, 1, 1000)) -- `1`
print(Math.clamp(500, 1, 1000)) -- `500`
print(Math.clamp(1000, 1, 1000)) -- `1000`
print(Math.clamp(9999, 1, 1000)) -- `1000`
```

### Math.**step**(edge : number, x : number) : number

Generates a step function by comparing `x` to `edge`. The returned value is `0` if `x < edge`, and `1` is returned otherwise.

### Math.**smoothstep**(edge0 : number, edge1 : number, x : number) : number

Interpolates `x` between `edge0` and `edge1`, smoothing at the limits as for a [sigmoid-like](https://en.wikipedia.org/wiki/Sigmoid_function) function. This is somewhat similar to `Math.lerp()`, but the interpolation will gradually speed up from the start and slow down toward the end. This is useful for creating natural-looking animation, fading and other transitions.

### Math.**smootherstep**(edge0 : number, edge1 : number, x : number) : number

Similarly to `Math.smoothstep()`, the function calculates an even *smoother* sigmoid-like interpolation of `x` between `edge0` and `edge1`, following [Ken Perlin](https://en.wikipedia.org/wiki/Ken_Perlin)'s suggestion.

### Math.**sign**(x : number) : number

Returns `-1` or `1` according to the sign of `x`. Note that this function **never** returns `0` as when dealing with (floating-point) numbers even the `0` has a negative or positive sign.

### Math.**signum**(x : number) : integer

Returns `-1`, `0`, or `1` whether `x` is less, equal, or greater than `0`.

### Math.**sincos**(rotation : integer) : number, number

Returns the **sine** and **cosine** for the angle `rotation` (expressed as integer in the (periodic) range `[0, 511]`).

### Math.**angle_to_rotation**(angle : number) : integer

Converts an angle, expressed in [radians](https://en.wikipedia.org/wiki/Radian) by the value `angle`, to a rotation amount in the range `[0, 511]`.

### Math.**rotation_to_angle**(rotation : integer) : number

Converts a rotation, expressed as integer in the range `[0, 511]` by the value `angle`, to an angle expressed in radians.

### Math.**invsqrt**(x : number) : number

Calculates the *inverse square root* of `x` as `1.0f / sqrtf(x)`. This can be optimized with the plain Lua code `x ^ -0.5`, however.

### Math.**finvsqrt**(x : number) : number

Calculates the *inverse square root* of `x`, using the famous [Quake's fast approximation](https://en.wikipedia.org/wiki/Fast_inverse_square_root).

> This function has been implemented mostly as **easter egg**. In a typical usage scenario, it should more efficient to calculate the inverse square root of a number `x` in native Lua code, as `x ^ -0.5` or `1 / math.sqrt(x)` (this former saves from the Lua-to-C context switch, but the latter is a specialized version).

### Math.**rotate**(x : number, y : number, rotation : integer) : number, number

Calculates the coordinates of the point `<x, y>` when two-dimensionally rotated by a rotation `rotation` (in the integer periodic range `[0, 511]`).
