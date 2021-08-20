---
layout: module
category: module
namespace: tofu.core
title: System
permalink: /modules/tofu.core/System/
---
# Usage

```lua
local System = require("tofu.core").System
```

## Functions

### System.**args**() : table

Returns a `table` with the command-line arguments passed to the engine executable at launch-time. This mimics the `argv` array for a C/C++ program, with the exception the first entry (the one indicating the executable itself) is not present.

### System.**version**() : integer, integer, integer

Return a *tuple* of three values stating the run-time version of the game engine (major, minor, and revision).

### System.**time**() : number

Returns the elapsed amount of seconds since the launch of the game-engine.

### System.**fps**() : integer

Returns the current frame-per-seconds counter, as moving average of the last `128` samples.

### System.**stats**() : number, number, number, number [^1]

Returns a *tuple* of **four** value, each indicating the time (in seconds) spent in a different part of the frame time: process, update, render, and (total) frame time. Like for the FPS, each value is filtered using a moving average of `128` samples.

### System.**heap**(type = "b" : string) : number [^1]

Returns the current heap usage amount. This is the *grand-total* of the memory used by the application. The optional argument `type` can be used to specify if the amount should be expressed in `b`ytes, `k`ilobytes, or `m`egabytes.

### System.**is_active**() : boolean

Tells whether the game-engine is the current active (i.e. focused) window. Can be used to automatically "pause" the game when the user switch to another application.

### System.**quit**()

Signals and halts the game-engine execution.

---

[^1]: These functions are available only in the `DEBUG` build.
