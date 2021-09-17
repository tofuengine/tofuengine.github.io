---
layout: guide
category: guide
title: File System
permalink: /guides/file-system/
order: 3
---
# File System

From within a **#tofuengine** project, the file access is *sandboxed*, i.e. isolated from the real machine's file-system and can access only a limited part of it (and mostly in read-only mode). This mean that one cannot simple try and access files from the specific (absolute) path, as all paths are relative to the current game working-directory. No harm can be done to the system, and no user private files can be accessed.

> As a safety measure Lua's standard `io` and `os` libraries aren't available.

Also, file paths are platform agnostic as the engine runtime adapts to the underling OS. However, UN*X convention is used to specify paths. For example, these are all valid paths

```lua
local Canvas = require("tofu.graphics").Canvas -- This is an internal pre-loaded module, `.` is required.

local Camera = require("lib.camera") -- Lua' standard module sub-path separator...
local Player = require("lib/player") -- ... or UN*X-like folder separator.

local background = Canvas.new("assets/background.png") -- We can't use the `.` here, but the path separator.
```

## Sandbox

## Packed files

Similar to Quake's PAK format. Uncompressed, fast access. No limit to filename length. Optional encryption.

## Mount points

## User folder
