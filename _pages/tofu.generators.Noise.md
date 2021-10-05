---
layout: module
category: module
namespace: tofu.generators
title: Noise
permalink: /modules/tofu.generators/Noise/
---
# Usage

```lua
local Noise = require("tofu.generators").Noise
```

## Constructors

### Noise.**new**(type : string = 'perlin', seed : number = 0.0, frequency : number = 1.0) : object

Constructs a noise generator given a type, a seed, and with a given frequency. `type` can be `perlin`, `simplex`, or `cellular`. When called without arguments, `perlin` will be used as a default type.

## Getters/Setters

### Noise:**seed**() : number

Gets the current noise generator seed. The default value is `0.0`.

### Noise:**seed**(seed : number)

Sets the noise generator seed. Any value is permitted.

### Noise:**frequency**() : number

Gets the current noise generator frequency. The default value is `1.0`.

### Noise:**frequency**(frequency : number)

Sets the noise generator frequency. When passing normalized coordinates to the `Noise:generate()` method, the `frequency` parameter assumes it's proper meaning and can be set to values greater than `1.0`. Otherwise, with not-normalized coordinates, the `frequency` parameter should be in the range `[0, 1]`.

## Methods

### Noise:**generate**(x : number, y : number = 0.0, z : number = 0.0) : number

Evaluates the noise function, called with up to **three** floating-point arguments, and using the current `seed` and `frequency` parameters. The returned value is in the range `[0, 1]`.

It is advisable (but not required) to pass normalized coordinates in the range `[0, 1]`. In that case, the `frequency` parameter assumes it's proper meaning and can be set to values greater than `1.0`. Otherwise, with not-normalized coordinates, the `frequency` parameter should be in the range `[0, 1]`.

> The object's meta-method `__call()` is mapped to this method and can be used as an alternative.
