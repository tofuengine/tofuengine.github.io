---
layout: module
category: module
namespace: tofu.graphics
title: Bank
permalink: /modules/tofu.graphics/Bank/
---
# Usage

```lua
local Bank = require("tofu.graphics").Bank
```

## Constants

### Bank.**NIL** : number

This constant is used to reference the first cell in the bank. It is, practically the same as passing `0` as a cell identifier.

## Functions

### Bank.**new**(canvas : object, cells : string) : object

Creates a new `Bank` object, using [`canvas`](/modules/tofu.graphics/Canvas/) as a sprite sheet. The logical positioning of the cells in the [sprite sheet](/guides/sprite-sheet/) is specified according to the content of the `cells` file.

### Bank.**new**(canvas : object, cell_width : number, cell_height : number) : object

Creates a new `Bank` object, using [`canvas`](/modules/tofu.graphics/Canvas/) as a sprite sheet. The bank cells will have an equally constant size of `cell_width` by `cell_height` pixels.

### Bank.**size**(cell_id : number, scale_x = 1.0: number, scale_y = scale_x : number) : number

### Bank.**blit**(canvas : object, x : number, y : number, cell_id : number)

### Bank.**blit**(canvas : object, x : number, y : number, cell_id : number, rotation : number)

### Bank.**blit**(canvas : object, x : number, y : number, cell_id : number, scale_x : number, scale_y : number)

### Bank.**blit**(canvas : object, x : number, y : number, cell_id : number, scale_x : number, scale_y : number, rotation : number, anchor_x = 0.5 : number, anchor_y = anchor_x : number)

### Bank.**tile**(x : number) : number
