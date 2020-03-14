# a2xtech

Vanilla engine, rewritten into C++ from VB6


# Frequently Asking Questions
This paragraph contains a list of several questions you would to ask me, I'll give answers to most of them.

## What is this?
It's a port of an old VB6 engine, purely written in C++. It reproduces an old engine completely (except an Editor), includes lots of its logical bugs (crashy bugs where they were found and then fixed).


## Why did you make it?
Why? I have several purposes for why I made it:
- It's a very convenient life model for research I want to use in PGE Engine development.
- To make it work without it being necessary to use Wine on non-Windows platforms and allow it to run on any other than x86 platforms.
- To be able to optimize it to make it use fewer hardware resources than the original VB6-based build of a game.


## You have PGE Engine, why you have spent an over than one month to craft this thing?
I need it for PGE Engine development directly, it's much easier to hack and inspect rather dealing with the old and inconvenient VB6 environment.


## What's future of PGE Engine as A2xTech now exist?
I'll continue development of PGE Engine as I still have to pass the second goal of PGE Project.
Since foundation, PGE Project had two goals: 1) save SMBX; 2) give a flexible toolkit for new platform games. Opening of SMBX sources and introducing the A2xTech has solved the first goal: SMBX has been saved and now it's free and opensource cross-platform software. PGE Engine will be used to pass the second goal - giving a toolkit for new games. Unlike A2xTech, PGE Engine gives a full flexibility that allows anyone to build something new from scratch without inheriting of an old game base. However, A2xTech is needed for PGE Engine as a working research model to develop a new engine. It will be similar to GZDoom and Chocolate Doom ports of the Doom game: GZDoom is a powerful and functional engine, the best choice of modders; a Chocolate Doom is an accurate port of the original game to a modern platform with a purpose to represent an original game including even bugs. The PGE Engine intends to be like a GZDoom while A2xTech is an analog of Chocolate Doom to represent an original game on modern platforms.


## How it will be useful for the SMBX2/LunaLua project?
SMBX2 leaders should choose the way of life: continue the project as-is with use of a clunky hacked EXE and be the biggest workaround in the universe; or make a fork of the A2xTech and make the major port of LunaLua experience into it which will make SMBX2 finally stop being a workaround over old SMBX and be just a standalone game. Potentially this thing will make any future DLL-injection hacks over the old EXE be useless: as we now have this thing, now it's possible to backport most of LunaLua base into this and get in the standalone game instead of an ugly unstable clunky cludge that we had to deal with over 6 years! Any features can be implemented directly over A2xTech's source code rather than crafting a dozen suspicious ASM hacks that are conditionally possible in comparison to direct source code hacking.


## How to use this?
Here are many ways to play games with it:
- there are some ready for use packages, just take and use as you did it with SMBX.
- [macOS users, skip this]: use by the same way as an original game: put an executable file into the game root folder with an "a2xtech.ini" that contains next text:
```
[Main]
force-portable = true
```
, music.ini, sounds.ini and additional "graphics/ui" folder. An important note: all default graphics must be converted into PNG, use GIFs2PNG tool from PGE Project over your "graphics" folder with a "-d" switch. Don't use "-r" switch to keep original GIFs together with new-made PNGs if you plan to continue the use of original VB6-written SMBX.
- use it for debug mode: in your home directory, create the ".PGE_Project/a2xtech" folder (on macOS the "~/Library/Application Support/PGE Project/a2xtech") where you should put a full set of game resources and worlds stuff, this folder will work like a game root in the original game. This mode allows you to run an executable file from any folder location of your computer and use the same location of resources for all builds (except these are marked as portable by an INI file).


## How to add custom episodes for the macOS version?
If you have a bundled build of A2xTech, all default resources are inside your .app: "Content/Resources/assets/". You can modify the content, but it's not recommended! Instead, after the first run of a game, in your home directory will appear the next directory:
```
   ~/A2xTech Episodes
```
In this directory, you will find an empty "battle" and "worlds" folder to put your custom stuff. At the "~/Library/Application Support/PGE Project/a2xtech" path logs, settings and game saves will be stored.
If you want to replace default assets with your own, you can modify the content of the app bundle or compile a new build with giving of the necessary CMake arguments which needed to pack your custom assets root and icon into the new bundle or make the assets-less build (if you give no arguments, the assets-less build will result). Therefore, you need to put the full content of the game root into the "~/Library/Application Support/PGE Project/a2xtech" folder, include default assets (graphics, music, sounds, intro and outro levels, default battle and worlds folders).


## What is different with this thing in comparison to the original VB6 build?
- First off, it's written in C++ while original (as we already know) is written in VB6.
- Doesn't have an Editor. Instead, in nearest future it will have a deep integration with PGE Editor that will allow to use it with the same functionality as in original editor (the "magic hand" functionality was kept to allow real-time editing of the level while testing, it's needed to use IPC communication with PGE Editor to get the ability to use it better).
- Full support of UTF-8 in filename paths and internal text data (original game had the only 8bit ANSI support).
- For graphics and controlling, it uses an SDL2 library while original game have used WinAPI calls and GDI library.
- It uses PGE-FL that has better file formats support.
- A support for WLDX world maps are allowing unlimited credits lines and custom music without it being necessary to use a music.ini for music replacements.
- Some LVLX exclusive features now working: vertical section wrap, two-way warps, custom "star needed" message, warp enter event, ability to disable stars printing in HUB episodes for specific doors, ability to disable interscene showing when going to another level through a warp.
- Built-in support for episide and level wide music.ini and sounds.ini to override default music and sounds assets.
- World maps now supports a custom directory to store any specific resources like custom tiles/scenes/paths/levels and not spam the episode root folder with wolrd map resources anymore.
- Default config format is INI, old config.dat format is no longer supported, mainly because of incompatible key code values (SDL_Scancode versus VirtualKeys enum of Windows API).
- Game saves now using the SAVX format instead of a classic SAV. However, if you already have an old gamesave, you still can resume your game by using a new engine now (next gamesave attempt will result a SAVX file, old gamesave in SAV format will be kept untouched).
- Built-in PNG support for custom and default graphics. Masked GIFs are still supported for backward compatibility, however, without making an unexpected auto-conversion like SMBX-38A does.
- Checkpoints now have multi-points! You can use them in your levels multiple times without limits!
- It does use of lazy-decompress algorithm to speed-up the loading of a game and reduce the memory usage.
- For music and SFX, the MixerX library is used to give a support for a wide amount of sound and music formats!
- It doesn't embeds any graphics: there are NO trurely hardcoded graphics, everything is now represented by external graphics!
- Some internal limits have been expanded.
- Built-in GIF recorder by F11 key (F10 on macOS, F11 is reserved by system UI for a "show desktop" action)


## How to build it?
To build it, you need to have next things:
- CMake
- Ninja optionally (to speeds-up the build process)
- Compatible C/C++ compiler (GCC, Clang, MSVC haven't tested yet)
- Git (required to pull submodules and clone source of dependent libraries to build them in place)
- Mercurial (required to clone an official SDL2 repository to build it in place here)
- Optionally: system-wide installed dependencies: SDL2, libFreeImageLite (a modded implementation of the FreeImage), MixerX sound library, AudioCodecs collection of libraries. Having them be installed in a system gives a major build speed up. However, it's possible to build all these dependencies in place here with a cost of extra build time being added.
