---
title: tutorial &#35;0
caption: tutorial &#35;0
layout: home
category: docs
permalink: /docs/tutorial-0/
---

# Our First Program

So, we are going to write our first program. Following a long-dated tradition, we will present a welcoming message to the user (that is, ourselves).

Every **Tofu** program is built-up *at the very least* of **two files**:

* `tofu.config`, and
* `main.lua`.

The first, unsurprisingly, holds the program instance parameters (e.g. display width and height). The second one, even more unsurprisingly, is the program entry-point script. For our example program, we will be using this configuration file (save it as `tofu.config` in a folder of your choice).

```ini
title=Hello, Tofu!
width=320
height=240
scale=0
fullscreen=false
exit-key-enabled=true
```

More details about the available configuration settings can be found in the [reference](/docs/configuration-file). For the moment, all we need to know is that with this configuration file we are going to request a `320x240` virtual-screen that will be auto-scaled to fit the physical display as much as possible (while retaining windowed-mode, i.e. we aren't going full-screen), window-title will be set to `Hello, Tofu!`, and *exit-key* (i.e. the `ESCAPE` keyboard key) will be enabled.

Now it's time to tackle the program entry-point. We need to write a Lua script returning a "class" adhering to a specific prototype (more on this [later](/docs/entry-point)). For the moment, just save the following script in the same folder you picked for the configuration file and name it `main.lua`.

```lua
-- Include the modules we'll be using.
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
  -- Get a reference to the default canvas (i.e. the the virtual-screen)...
  local canvas = Canvas.default()

  -- ... and clear it w/ default background palette color (i.e. palette index #0).
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

Now, launch the application with the following command

```bash
./tofu ./hello-tofu
```

or with

```bash
./tofu
```

if the `tofu.config` and `main.lua` files both reside in the same folder as the engine executable.

When you are done beholding our first program, exit by pressing the `ESCAPE` keyboard key.

[continue >>](/docs/tutorial-1)