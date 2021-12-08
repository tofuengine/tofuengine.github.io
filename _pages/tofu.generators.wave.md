---
layout: module
category: module
namespace: tofu.generators
title: wave
permalink: /modules/tofu.generators.wave/
---
# Usage

```lua
local Wave = require("tofu.generators.wave")
```

## Constructors

### Wave.**new**(form : string, period = 1.0 : number, amplitude = 1.0 : number) : object

Returns a `Wave` object, with period `period`, that maps a floating-point value to the range `[-amplitude, amplitude]`. `form` can be one of the following values: `sine`, `square`, `triangle`, `sawtooth`.

## Getters/Setters

### Wave:**form**() : string

Gets the string representation of `Wave` object waveform.

### Wave:**form**(time : string)

Gets the current waveform bound of this `Wave` object.

### Wave:**period**() : number

Gets the `Wave` object waveform's period. The default value is `1.0`.

### Wave:**period**(period : number)

Sets the `Wave` object waveform's period.

### Wave:**amplitude**() : number

Gets the `Wave` object waveform's amplitude. The default value is `1.0`.

### Wave:**amplitude**(amplitude : number)

Sets the `Wave` object waveform's amplitude.

## Methods

### Wave:**at**(time : number) : number

Evaluates the wave function at `time` and returns the value. `time` can be any value but it is advisable to keep it in the range `[0, period)` to increase accuracy on the long time. The returned value is in the range `[-amplitude, amplitude]`.

> The object's meta-method `__call()` is mapped to this method and can be used as an alternative.
