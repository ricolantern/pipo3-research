# pipo3-research (Ape Escape 3 Research)
A solo project that contains research findings and commentary based on reverse engineering done for educational purposes under Dutch law ([View translation here](https://www.wipo.int/wipolex/en/legislation/details/17868)).

The main goal is to use the found knowledge to re-construct the game in question, using its original assets and my own code utilizing the [Godot Engine](https://godotengine.org/).
The results of which will not be made publicly available, but documented in indirect formats instead (video, sound, plain text, etc).

Despite my prior experience in game development & programming, this project is my first step into reverse engineering.
Please adjust your expectations accordingly.
## Specifications
| Spec | Description |
| --- | --- |
| _Game Name_ | Ape Escape 3 / Saru Get You 3 / サルゲッチュ3 |
| _Game Region_ | NTSC-J (For code & file decomp) / USA (For english assets) |
| _Current Focus_ | Reverse engineering code related to the .i3d format |
## Toolset
| Tool | Description |
| --- | --- |
| _[Ghidra 11.4.2](https://github.com/NationalSecurityAgency/ghidra/releases/tag/Ghidra_11.4.2_build)_ | Primary research tool used to decompile & snoop through the game's files. |
| _[Ghidra Emotion Engine: Reloaded](https://github.com/chaoticgd/ghidra-emotionengine-reloaded)_ | Ghidra extension that introduces a wide variety of support for PS2 disassembly & decompilation. |
## Index
- [Ghidra notes](https://github.com/ricolantern/pipo3-research/blob/main/docs/GhidraNotes.md)
## Interesting Finds
### The Game Engine
Codenamed "BULLETS" -- Sony's in-house game engine, strongly suggested to have been used to develop AE3 and various other titles from around that timeframe.
1. _Saru Get You! SaruSaru Big Mission_ seems to have been built directly off of, or at least reuses large portions of AE3, not limited to just assets.
   - TODO
1. _Saru Get You! SaruSaru Big Mission_ exposes a portion of the source code filetree, which revealed the engine name that was likely also used to develop AE3.
   - _Roughly a dozen strings like this are present, most interestingly in the context of reversing the i3d format: `c:/BULLETS/sarup2/src/Minigames/CKI3DUtl.cpp`_
     - _`BULLETS`_
       - Game engine codenames are usually written in all-caps.
       - It's pretty common, even nowadays, to parent game projects to a folder that indicates which engine it's made with.
       - Unfortunately so far sarusaru is the only game I can find in AE3's timeframe that exposes the filetree from this far up.
     - _`sarup2`_
       - `saru` = All ape escape projects start with "saru" by tradition. AE3's codename is "saru3".
       - `p` = Portable.
       - `2` = Likely refers to it being the 2nd saru-related project developed for the PSP. (I checked Pipo Saru Racer, but the only hints I can find of a project name there is a string `"ms0:/PSP/saru_racer"`, so no "sarup" or "sarup1")
