# Ghidra Notes
Areas of interest for further research.
Contents are technical and in the context of Ghidra.
## _Quick notes/todos for later_
- .i3d format references in strings, locations 006ca3f0 and 006ca3a7 (`?RemoraObjectImpl::RemoraObjectImpl(const simd::Octaword&, Object*)`) are interesting, exposing some hints about the internal animation system it seems?
- Tons of strings like `my:AnimationStart` and others that begin with "my:", according to AI, indicate that it's part of the internal data-driven animation/event system (go figure) defined in XML-like files. Most notably, it also suggests the "my" portion is a namespace that likely refers to something like "movie" or better yet, "Maya" (as in, pre-autodesk Maya).
- All display strings for the debug menu are present (but according to [this video](https://www.youtube.com/watch?v=kqsBNmCSZWU) they don't display at all for some reason. They're also slightly different from what this video displays). Create a patcher to restore these strings and add indicators to those that cause a crash.
- `Tim2` is referenced (006e6320 `void Tim2::initialize(int, int, const char*)`) among other tim2 strings. This is likely the (sole?) image format used in the game.
- `Mpeg2` is referenced (006e6268 `void Mpeg2Stream::initialize(const char*, int, int, bool)`) for pre-rendered cutscene use.
- What's a "DashBall" (006f86d0)? Some rendition of the dash ring gear or maybe an early name?
- There's a copyright notice for zlib (`" inflate 1.2.1 Copyright 1995-2003 Mark Adler "`). This likely means that the assets come pre-compressed and are then decompressed at runtime using zlib.
  - https://zlib.net/fossils/
- `xml=http://www.w3.org/XML/1998/namespace` is mentioned.
- There's a copyright notice for the Lua version used for dynamic editing of properties. The exact version is `Lua 5.0 Copyright (C) 1994-2003`.
- The build date for the Japan release is `"2005/06/21,14:49:06"`
- `sg2vab.c` is referenced as a string (what isn't at this point???).
  - sg2 = "Sound Group 2"
  - vab = "Voice-Attribute Bank" (.VAB, .VH, .VB)
    - contains instrument definitions + ADPCM samples??
    - VABp headers.
- Are these formats relevant (00704ca8)?

## _Game SDK version strings_
Defined Strings search on "PSII" reveals a handful of strings that detail the exact version of some of the SDK libraries the game uses for interacting with the hardware.
This information might also give us somewhat of an estimation as to which development kits were used in development, and perhaps even help in narrowing down early builds of the game??

Information about these libraries seems to be scarce to come by, and it should also be noted that your web searches may be confused with the community-driven PS2SDK project.
Care has been taken to ensure the information below is drawn from either official PS2 documentation archives, or otherwise inferred from the decompilation.
| Location | String Representation | (Inferred) Meaning | Library Description |
| --- | --- | --- | --- |
| 00678740 | "PsIIlibcdvd 3000" | PS2 CD/DVD Library | No official docs available. Suggested to be CD/DVD interactivity due to 006fe9f0 mentioning a function `CdDiskReady`. |
| 0067c4f0 | "PsIIlibpad2 3020" | PS2 (Controller) Pad Library 2 | Interacting with the DualShock controller(s). It's predecessing library documentation can be found [here](https://archive.org/details/ps-2-programmer-tool-runtime-library-controller-library). I'm unable to find an archive for libpad2. |
| 0067c560 | "PsIIlibdbc  3020" | PS2 Debug Channel Library | Defined Strings search on "dbc" reveals several output strings mentioning sockets and RPC. The string "sceDbcGetDeviceStatus: rpc error" suggests this was probably used to communicate with a dev kit. |
| 0067c578 | "PsIIspu2mem 3000" | PS2 SPU I/O | Used for memory transfers related to sound, as suggested by 006f10b0 (`static void SoundSys::load2spu(const char*, unsigned int)`) |
| 0067f9b0 | "PsIIlibkernl3000" | PS2 Kernel Library | Self explanatory. Used for interactions with the PS2 kernel. |
> [!NOTE]
> Look into the specifics of the .irx files.
## _Exposed source code strings_
There's a crap ton of strings formatted that scream they are properties, constants, events, enums, and even function definitions that include return & argument types.
Can prove to be immensely useful in the decompilation.

Game engines like Unity & Godot allow exposing properties into the engine's inspector window by serializing them, for ease of access by designers & other non-programmers.
Something similar to this may be the reason why all of these strings are here.
> [!NOTE]
> Think of a plan of approach. Could be good to extract all of these strings, categorizing them, and using them as cross-reference in making sense of the decomp. Likely need to write a script for this.
## _i3d file format_
- Header strings exist:
  - `I3D_BIN` (006fd0f8) = Model + bones?
  - `I3D_I3M` (006fd190) = Animation?
    - 0039e780 contains 4 consecutive pointer fixups likely representing offsets inside the i3d file. what does each refer to?
  - `I3D_I3C` (006fd198) = ??? (guessing collisions)
> [!NOTE]
> Tracing these strings (currently focused on I3M) so far seems to lead up to the I3M loading procedures.
> When do zlip deflate algorithms come into play?
