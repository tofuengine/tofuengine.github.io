---
layout: guide
category: guide
title: Project Structure
permalink: /guides/project-structure/
order: 2
---
# Project Structure

As hinted in the [Getting Started](/guides/getting-started/) page, each **#tofuengine** project is expected to have a well-defined structure to be successfully recognized. That is, some files need to be located in the project's root folder and have a predefined specific name in order for things to work, that is

* `tofu.config`,
* `main.lua`.

Let's see in more detail the content of those files.

# Configuration File

The `tofu.config` file is used to configure the general behaviour of a game project. The file structure carries some resemblance with [.ini files](https://en.wikipedia.org/wiki/INI_file) in that each line can be either:

* a key/value pair (i.e. two strings separated by the `=` character),
* a line-comment (i.e. starting with the `#` character and ending with a new-line), or
* a section indicator (i.e. a single identifier enclosed within `[` and `]`).

A key/value pair get its proper meaning according to the section where it appears. There's no predefined and required order for the configuration options to appear in the file, but take care in locating each key/value pair in its proper section. A section can appear multiple times in the same file, i.e. the configuration parameter context can be switched multiple times, if wanted. If a property appears multiple times, the last occurrence will define the actual value. Also, whitespace are significant, so bear this in mind when editing the configuration file.

A typical (complete) configuration file is the following:

```ini
[system]
identity=
version=0.10.0
debug=true
icon=icon.png
mappings=gamecontrollerdb.txt
[display]
title=.: Tofu Engine :.
width=320
height=240
scale=0
fullscreen=false
vertical-sync=false
effect=effect.glsl
[audio]
device-index=-1
master-volume=1.0
[keyboard]
enabled=true
exit-key=true
[cursor]
enabled=true
hide=true
speed=128.0
[gamepad]
enabled=true
sensitivity=0.5
inner-deadzone=0.25
outer-deadzone=0.0
emulate-dpad=true
emulate-cursor=true
[engine]
frames-per-seconds=60
skippable-frames=3
frames-limit=0
```

## Sections

### system

* `identity : string` (default to the alphanumeric representation of the display title)
* `version : string` (default to the current engine version)
* `debug : boolean` (default to `true`)
* `icon : string` (default to `icon.png`)
* `mappings : string` (defaul to `gamecontrollerdb.txt`)

### display

* `title : string` (default to `.: Tofu Engine :.`)
* `width : number` (default to `320`)
* `height : number` (default to `240`)
* `scale : number` (default to `0`)
* `fullscreen : boolean` (default to `false`)
* `vertical-sync : boolean` (default to `false`)
* `effect : number` (default to `effect.glsl`)

### audio

* `device-index : number` (default to `-1`)
* `master-volume : number` (default to `1.0`)

### keyboard

* `enabled : boolean` (default to `true`)
* `exit-key : boolean` (default to `true`)

### cursor

* `enabled : boolean` (default to `true`)
* `hide : boolean` (default to `true`)
* `speed : number` (default to `128.0`)

### gamepad

* `enabled : boolean` (default to `true`)
* `sensitivity : number` (default to `0.5`)
* `inner-deadzone : number` (default to `0.25`)
* `outer-deadzone : number` (default to `0.0`)
* `emulate-dpad : boolean` (default to `true`)
* `emulate-cursor : boolean` (default to `true`)

### engine

* `frames-per-seconds : number` (default to `60`)
* `skippable-frames : number` (default to `3`)
* `frames-limit : number` (default to `0`)

# Entry-point

# Fragment shaders

