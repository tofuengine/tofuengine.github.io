---
layout: guide
category: guide
title: File System
permalink: /guides/file-system/
order: 3
---
# File System

For a **#tofuengine** application the file I/O is *sandboxed*. The application runs isolated from the real machine's file-system and can access only a limited part of it (and almost exclusively in read-only mode). This is because all paths are relative to the current game mount-points (more on this later). One cannot simple try and access files with a specific (absolute) path, or try and move to the parent folders (the `.` and `..` entries are forbidden, for simplicity, as not supported by packed files) as the operation is not allowed. As an additional safety measure, Lua's standard `io` and `os` libraries are unavailable. No harm can be done to the system, and no user private files can be accessed.

File paths are platform agnostic, as the engine runtime adapts and maps them to the underling OS requirements (e.g. composing and converting the path separators as needed). However, UN*X convention is used to specify paths. For example, these are all valid paths

```lua
local Canvas = require("tofu.graphics").Canvas -- This is an internal pre-loaded module, `.` is required.

local Camera = require("lib.camera") -- Lua' standard module sub-path separator...
local Player = require("lib/player") -- ... or UN*X-like folder separator.

local background = Canvas.new("assets/background.png") -- We can't use the `.` here, but the path separator.
```

When using Lua's `require` function to load custom modules both `.` and `/` are valid path-separators. It boils down to a matter of personal choice, but *be consistent* in using one or another or the module could be potentially be duplicated in the modules' *preloaded* table.

## Mount points

Upon start, the engine configures its *base-path*, either by determining it from the current working directory (i.e. the folder into which the executable is contained) or through the `--path` command-line option. The content of this folder is scanned in alphabetical order and every valid **packed** file is added as a mount-point. Finally, the base-path is added to the (virtual) file-system *search-path*, too.

> The order with which the entries are added is important, as newer entries *overrides* the older ones (with *base-path* having the highest priority). This permits the concept of *modding*, i.e. adding a file/archive that specify a new content to be used instead of the original one. 

## Packed files

Following a long dated tradition (when disk space mattered and cluster's internal fragmentation was an issue), **#tofuengine** supports a *packed* file format. It's a relatively simple, uncompressed, fast-access file-format with optional encryption[^1]. It's main usage is to help the final product organization and distribution.

Package file can be generated with the `pakgen.lua` script. By launching the script, a folder can be scanned and "converted" into an single-file representation (i.e. an archive) of it.

## User folder

TBD.

[^1]: The encryption algorithm is long from being military grade. :)