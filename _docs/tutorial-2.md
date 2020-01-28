---
title: tutorial &#35;2
caption: tutorial &#35;2
layout: home
category: docs
permalink: /docs/tutorial-2/
published: false
---

# Custom fonts

In the previous examples we were using one of the [default monochrome fonts](api/graphics/font) (most notably, a `5x8` sized font). Apart the engine-provided ones, custom monochrome or multi-color fonts can be dynamically loaded.

```lua
-- Include the modules we'll be using.
local System = require("tofu.core").System
local Canvas = require("tofu.graphics").Canvas
local Display = require("tofu.graphics").Display
local Font = require("tofu.graphics").Font
local Class = require("tofu.util").Class

-- The entry point is a class, we are creating with a helper function.
local Main = Class.define()

-- The message we are displaying, as a "constant".
local MESSAGE = "Hello, Tofu!"

function Main:__ctor()
  -- Load a predefined palette, we choose Pico-8's one.
  Display.palette("pico-8")

  -- Load a custom 8x8 font from file, setting palette color `0` as background
  -- and `15` as foreground.
  -- Please note that, as default, palette color `0` is set as transparent. This
  -- means that the font background color won't be drawn.
  self.font = Font.new("assets/font-8x8.png", 8, 8, 0, 15)
end

function Main:input()
  -- Nothing to do, here.
end

function Main:update(_)
  -- Ditto.
end

function Main:render(_)
  -- Get a reference to the default canvas (i.e. the the virtual-screen).
  local canvas = Canvas.default()

  -- Query current time since the start, expressed in seconds (as a floating point number).
  local t = System.time()

  -- Clear the virtual-screen with default background color (i.e. palette color #0).
  canvas:clear()

  -- Query for text width/height and calculate the (screen-centered) origin
  -- x/y position.
  local canvas_width, canvas_height = self.canvas:size()
  local text_width, text_height = self.font:size(MESSAGE)
  local x, y = (canvas_width - text_width) * 0.5, (canvas_height - text_height) * 0.5

  -- Query for font char width/height, we'll use it for offseting the characters.
  local char_width, char_height = self.font:size()

  -- Scan the message text one char at time. We need the current char index in order
  -- to change color for each character.
  for i = 1, #MESSAGE do
    -- Compute the verical offset using a sine wave, each chacter with a different value.
    local dx = (i - 1) * char_width
    local dy = math.sin(t * 2.5 + dx * 0.05) * char_height

    -- Convert the time to an integer (speeding it up a bit) and get a different
    -- color for each character. Then instruct the engine that color `15` need to be
    -- remapped to color `index`.
    local index = (tonumber(t * 5) + i) % 16
    canvas:shift(15, index)

    -- Draw the i-th character, accounting for vertical offset.
    self.font:write(MESSAGE:sub(i, i), x + dx, y + dy)
  end
end

return Main
```

Please note that we are not required pass a color in the range `[0, 15]` (remember, we are using 16 colors palette), as the engine automatically filters it with a modulo operator (i.e. color index `16` will be interpreted as color index `0`).

Once a palette color as been "shifted" it remains such as long as it's changed again or the `Canvas.reset()` function is called (which reset the drawing context to the initial state). In the next tutorial we will learn how to selectively shift colors without interfering with other draw operations.

[continue >>](/docs/tutorial-3)
