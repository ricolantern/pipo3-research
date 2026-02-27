# Strings
Interesting finds after going through all of the game's strings left in the code.
This is a work in progress.
## The Engine
Playing _SaruSaru Big Mission_ makes it very obvious that it's a heavily modified version of _Ape Escape 3_.
Even moreso, string searching through the game's code makes it apparent a lot of logic was reused, including the I3D model format.

Many strings in _Ape Escape 3_ are file paths relative to the project's filesystem, but none go further back up than the project's codename "saru3".
_Big Mission_ is an exception. There is at least one string that prepends "saru3" with **"BULLETS"**.
We can argue that this is the name of the engine used internally at Sony due to how it's common--even nowadays--to parent projects to a folder that indicates the engine, for proper grouping of projects.

Throwing a few of Sony's games into Ghidra from around the time _Ape Escape 3_ was being developed show strong indicators all of the below share the same engine:
- Ape Escape 3
- SaruSaru Big Mission
- Ape Escape Racing
- Genji: Dawn of the Samurai
- ...possibly more

This is important to know, because this means reversing one game's format also reverses that of another (with minimal modifications).
> [!NOTE]
> **TODO:** _Take a peek at other Sony games from around the game's launch date not listed above._
## Model Format
Unpacking the game's assets shows that the 3d models are suffixed with "i3d".
Internally, the game has three file headers to differentiate the type of i3d file the game is dealing with:
| Header | Meaning | Contains |
| ---- | ---- | ---- |
| I3D_BIN | "Binary container" -- possibly just a general term for "here be the main data" | Mesh, skin, rig. |
| I3D_I3M | "Motion" | Animation data. 1 file = 1 animation. |
| I3D_I3C | "Collision" | Collision data. |

Interestingly, _Ape Escape 3_ so far seems to have been one of, if not the earliest application of the i3d format.
This can be inferred from how every format -- mesh, animation, collision -- are all stored in files suffixed with "i3d" rather than their own variant counterparts
(e.g. a sane developer would want to be able to identify an animation file by a "i3m" suffix instead of "i3d"!)
All of the games listed in [The Engine](#the-engine) section above properly split their files into their variant counterparts, but Ape Escape 3 is the sole outlier.
> [!NOTE]
> **TODO:** _Other games listed above use new i3d variant headers I3R (rig?), I3S (skin?). Document these._
## Image Format
Like many PS2 games, Ape Escape 3 uses the TIM2 image format.
TIM2 has the ability to store multiple quality levels of the same image, which the engine can switch between based on the distance between (presumably) the camera and the rendered object its displayed on.
Interestingly, _Genji: Dawn of the Samurai_ contains a string "OPTPiX iMageStudio 3"... Which yes, is actually a 3rd party tool likely used in the development of the aforementioned game!
It is still possible to download and run this software on Windows 10 (I can confirm!) and it natively allows one to view and edit TIM2 files directly -- including the quality levels mentioned earlier.
While we can only guess this software was also used in the development of _Ape Escape 3_, it's more intriguing to note that this software allows for easy viewing & editing of _Ape Escape 3_'s image files.
