---
layout: module
category: module
namespace: tofu.generators
title: tweener
permalink: /modules/tofu.generators.tweener/
---
# Usage

```lua
local Tweener = require("tofu.generators.tweener")
```

## Constructors

### Tweener.**new**(easing : string, duration = 1.0 : number, from = 0.0 : number, to = 1.0 : number) : object

Constructs a tweener object that transforms a floating-point according to a specified rate of change. The input range is `[0, duration`]. The output range is `[from, to]`. `easing` is an [easing function](https://easings.net/), and can be one of the values in the table below.

| :---                 | :---                 | :---                 |
| `linear`             |                      |                      |
| `quadratic-in`       | `quadratic-out`      | `quadratic-in-out`   |
| `cubic-in`           | `cubic-out`          | `cubic-in-out`       |
| `quartic-in`         | `quartic-out`        | `quartic-in-out`     |
| `quintic-in`         | `quintic-out`        | `quintic-in-out`     |
| `sine-in`            | `sine-out`           | `sine-in-out`        |
| `circular-in`        | `circular-out`       | `circular-in-out`    |
| `exponential-in`     | `exponential-out`    | `exponential-in-out` |
| `elastic-in`         | `elastic-out`        | `elastic-in-out`     |
| `back-in`            | `back-out`           | `back-in-out`        |
| `bounce-out`         | `bounce-in`          | `bounce-in-out`      |

## Getters/Setters

### Tweener:**easing**(easing : string)

Sets the `Tweener` easing function (see the table above for the supported values).

### Tweener:**easing**() : string

Gets the string representation of the current easing function used by the `Tweener` object.

### Tweener:**duration**(duration : number)

Sets the amount of time, typically in seconds, the `Tweener` takes to go from `from` to `to`.

### Tweener:**duration**() : number

Gets the duration of the `Tweener`.

### Tweener:**range**(from : number, to : number)

Sets the interval of values onto which the `Tweener` evaluates, i.e. the output range of the easing function.

### Tweener:**range**() : number, number

Returns a pair of `number` values, telling the range `[from, to]` used as an output for the easing function of the `Tweener` object.

## Methods

### Tweener:**evaluate**(time : number) : number

Transforms a floating-point according to the current object [easing function](https://easings.net/). `time` should be in the range `[0, duration`]. The return value range is `[from, to]`.

> The object's meta-method `__call()` is mapped to this method and can be used as an alternative.
