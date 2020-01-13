---
title: tutorial
caption: tutorial
layout: home
category: docs
permalink: /docs/tutorial/
---

# Our First Program

So, we are going to write our first program. Following a long-dated tradition we will present a welcoming message to the user (that is, ourselves).

Every **Tofu** program is built-up *at the very least* of **two files**:

* `tofu.config`, and
* `main.lua`.

The first, unsurprisingly, contains the program instance parameters (e.g. display width and height). The second one, even more unsurprisingly, is the program entry-point script. For our example application we will be using this configuration file (save it as `tofu.config` in a folder of your choice).

```ini
title=Hello, Tofu!
width=256
height=64
scale=0
fullscreen=false
exit-key-enabled=true
```

More details on the available configuration settings can be found in the API reference. For the moment, all we need to know is that with this configuration file we are going to request a 256x64 virtual-screen that will be auto-scaled in window-mode (i.e. w/o going full-screen), with a custom title `Hello, Tofu!`, and the *exit-key* (i.e. the ESCAPE keyboard key) will be enabled.

Again, save the following script in the same folder you picked for the configuration file.

```lua
-- Include the modules we'll be using.
local System = require("tofu.core").System
local Canvas = require("tofu.graphics").Canvas
local Font = require("tofu.graphics").Font
local Class = require("tofu.util").Class

-- The entry point is a class, we are creating with a helper function.
local Main = Class.define()

-- The message we are displaying, as a "constant".
local MESSAGE = "Hello, Tofu!"

function Main:__ctor()
  -- Load a predefined palette, we choose Pico-8's one.
  Canvas.palette("pico-8")

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
  -- Clear the virtual-screen with palette color #0.
  Canvas.clear(0)

  -- We need the font (message) width and height to center it on screen.
  local font_width = self.font:width(MESSAGE)
  local font_height = self.font:height()

  -- Compute vertical and horizontal position for the text.
  local x = (Canvas.width() - font_width) * 0.5
  local y = (Canvas.height() - font_height) * 0.5

  -- Finally, draw the message on-screen at the given position.
  self.font:write(MESSAGE, x, y)
end

return Main
```

Now, we can finally launch the application with the following command

```bash
./tofu ./hello-tofu
```

or

```bash
./tofu
```

if the `tofu.config` and `main.lua` files resides in the same folder as the engine executable.