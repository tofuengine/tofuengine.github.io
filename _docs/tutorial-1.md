---
title: tutorial &#35;1
caption: tutorial &#35;1
layout: home
category: docs
permalink: /docs/tutorial-1/
---

# Spicing up a bit

So far, so good... but also quite boring.

Since we are using a monochrome font, let's find out how to change color dynamically.

As you might have noticed, the foreground color for the font is specified in the font instance constructor `Font.default()`. The naive approach would be to create a new font with a different background/foreground every time we need it. Sure it will work, but would also be quite inefficient.

A better solution is to leverage **palette shifting**, that is the dynamic remapping of colors upon drawing. In our example we are using palette color `15` as a foreground color. We will be modifying the example to that every second the text color changes across the whole palette.

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

  -- Create a default font, palette color `0` as background and `15` as foreground.
  -- Please note that, as default, palette color `0` is set as transparent. This
  -- means that the font background color won't be drawn.
  self.font = Font.default(0, 15)
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

  -- Convert the time to an integer, then instruct the engine that color `15` need to be
  -- remapped to color `index`.
  local index = tonumber(t) % 16
  canvas:shift(15, index)

  -- Clear the virtual-screen with default background color (i.e. palette color #0).
  canvas:clear()

  -- Get the canvas width and height.
  local canvas_width, canvas_height = canvas:size()

  -- We need the font (message) width and height to center it on screen.
  local text_width, text_height = self.font:size(MESSAGE)

  -- Compute vertical and horizontal position for the text.
  local x = (canvas_width - text_width) * 0.5
  local y = (canvas_height - text_height) * 0.5

  -- Finally, draw the message on-screen at the given position.
  self.font:write(MESSAGE, x, y)
end

return Main
```

Please note that we are not required pass a color in the range `[0, 15]` (remember, we are using 16 colors palette), as the engine automatically filters it with a modulo operator (i.e. color index `16` will be interpreted as color index `0`).

Once a palette color as been "shifted", the change remain active as long as it's changed again or the `Canvas.reset()` function is called (which reset the drawing context to the initial state). In the next tutorial we will learn how to selectively shift colors without interfering with other draw operations.

In the above code, we have explicitly calculated the target position of the text. Not a rocket-science problem, but it can rapidly become a hassle when done repeatedly. For this purpose, the engine comes in aid by providing a text alignment feature. We can align vertically/horizontally the text pivoting it around a specific point. Also note that we don't need to calculate the canvas center position by ourselves, but we can use the `Canvas.center()` method.

```lua
function Main:render(_)
  -- Get a reference to the default canvas (i.e. the the virtual-screen).
  local canvas = Canvas.default()

  -- Query current time since the start, expressed in seconds (as a floating point number).
  local t = System.time()

  -- Convert the time to an integer, then instruct the engine that color `15` need to be
  -- remapped to color `index`.
  local index = tonumber(t) % 16
  canvas:shift(15, index)

  -- Clear the virtual-screen with default background color (i.e. palette color #0).
  canvas:clear()

  -- Ask for the center position, which the canvas can provide ready-to-be-used.
  local x, y = canvas:center()

  -- Finally, draw the message on-screen at the given position, centering both
  -- vertically and horizontally.
  self.font:write(self.font:align(MESSAGE, x, y, "center", "middle"))
end
```

In the next tutorial we will be customizing the font.

[continue >>](/docs/tutorial-2)
