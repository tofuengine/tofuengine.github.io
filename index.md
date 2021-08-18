---
title: Home
layout: default
permalink: /
---
# Welcome!

**Tofu Engine** is a *free and open* self-contained game-engine suitable for small-to-mid 2D projects.

The engine can be considered a *perpetual work-in-progress* project of mine, with continuous additional features and updates. The *core* API, however, can be considered stable. 

## Highlights

* Carefully crafted C99 code.
* Self-contained, no additional runtime modules/libraries required (system-wide libraries excluded).
* Multi-platform support through cross-compilation (Windows, Linux and [Raspberry-Pi](https://www.raspberrypi.org/) -- macOS is currently not supported, possibly WebAssembly in the not so distant future).

## Features

* Fully scripted in [Lua](https://www.lua.org/).
* Straight multimedia support, no intermediate third-party libraries (OpenGL 2.1 required).
* Windowed/fullscreen display with best-fit integer automatic scaling.
* Internal software renderer. OpenGL is used only to present the framebuffer to the user (and apply post-process effects).
* Fixed- and variable-size *Blitter OBjects* drawing with rotation/scaling/flipping.
* Support for both proportional and non-proportional bitmap based fonts (alphabet subset can be specified, if required).
* Sprite batching for optimized (ehm) batch drawing.
* Tiles drawing with offset/scaling/flipping.
* Palette based graphics with up to 256 colors.
* Banked palette support w/ color bias during VRAM transfer.
* Predefined library of 8/16/32/64 colors palettes.
* Automatic nearest-matching-color palette indexing of [RGBA8888](https://en.wikipedia.org/wiki/RGBA_color_model) images.
* Per-color re-indexing (*shifting*) and transparency, affecting drawing operations (both per-draw and during VRAM transfer).
* Multiple canvas, with drawing state stack support.
* SNES' Mode7-like transforms, with scanline based ([HDMA](https://wiki.superfamicom.org/grog's-guide-to-dma-and-hdma-on-the-snes)) changes.
* Amiga's Copper-like programs, with pixel-wide resolution.
* Image programmable copy functions, to implement *script-shaders*.
* Image stencil copy function, with used definable *threshold function*.
* Image blend copy, with user definable *blending function* (`repeat`, `add`, `sub`, `multiply`, `min`, `max`).
* Post-effect display-wise fragment shaders.
* Library of "retro-feel" post-effects (LCD, CRT, color-blindness, etc...).
* Audio support w/ real time sound streaming on a separate thread.
* On-the-fly audio mixing w/ per voice looping/panning/balance/gain/speed control.
* Static and streamed audio data playback (FLAC format).
* Module playback support (MOD, S3M, XM, and IT).
* Out-of-the-box timers support.
* Ready-to-use 2D vector class and higher-order iterators.
* Customizable application icon.
* Support for *archived games*, via custom "packed" format (w/ optional encryption). Multiple archives are supported, with root folder ovde.
* Resource manager w/ caching I/O and single instance object loading/reuse.
* Game-controller support (w/ D-PAD and mouse emulation) w/ keyboard/mouse fallback if not available.
* Screen capture and recording.
* Framebuffer offsetting (e.g. for screen-shaking effect).
* Out-of-the-box 'tweening functions support (optimized [Penner's](http://robertpenner.com/easing/) set).
* Logging facility (w/ selectable severity level).
* Run-time signature check for Lua's API functions (debug build). Also, UDTs are typed-checked with a custom [RTTI](https://en.wikipedia.orki/Run-time_type_information) implementation.
* Crash screen (debug build).
* Game window focus detection (for game-pause).
* Real-time performance statistics (FPS and frame times) and resource usage (memory).
* User-dependent I/O functions to load/store game data.
* Configuration override through command-line arguments.

## Inspirations

**Tofu Engine** is an *original software*, result of the experience gained from ~30 years in programming on a broad range of platforms (some concept even stems back to *ancient* platforms like the [Amiga](https://en.wikipedia.org/wiki/Amiga) and the [SNES](https://en.wikipedia.org/wiki/Super_Nintendo_Entertainment_System), and *arcane* languages like [AMOS](https://en.wikipedia.org/wiki/AMOS_(programming_language)) and [Blitz BASIC 2](https://en.wikipedia.org/wiki/Blitz_BASIC)). However, it has also been influenced by modern similar/other softwares in one way or another.
