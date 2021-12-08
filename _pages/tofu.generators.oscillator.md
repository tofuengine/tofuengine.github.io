---
layout: module
category: module
namespace: tofu.generators
title: oscillator
permalink: /modules/tofu.generators.oscillator/
---
# Usage

```lua
local Oscillator = require("tofu.generators.oscillator")
```

## Constructors

### Oscillator.**new**(form : string, period = 1.0 : number, amplitude = 1.0 : number) : object

Returns an `Oscillator` object, with period `period`, that maps a floating-point value to the range `[-amplitude, amplitude]`. `form` can be one of the following values: `sine`, `square`, `triangle`, `sawtooth`.

## Methods

### Oscillator:**advance**(delta_phase : number)

Update the oscillator phase while keeping it restrained in the range `[0, period)` so that precision isn't lost as the oscillator's phase becomes greater.

### Oscillator:**value**(offset : number = 0) : number

Returns the current oscillator value, by optimally offsetting the current phase value. The returned value is in the range `[-amplitude, amplitude]`.

> The object's meta-method `__call()` is mapped to this method and can be used as an alternative.
