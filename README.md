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
| _Game Region_ | NTSC-J (For code & file decomp) / NTSC-U (For english assets) |
| _Current Focus_ | Reverse engineering code related to the .i3d format |
## Toolset
| Tool | Description |
| --- | --- |
| _[Ghidra 11.4.2](https://github.com/NationalSecurityAgency/ghidra/releases/tag/Ghidra_11.4.2_build)_ | Primary research tool used to decompile & snoop through the game's files. |
| _[Ghidra Emotion Engine: Reloaded](https://github.com/chaoticgd/ghidra-emotionengine-reloaded)_ | Ghidra extension that introduces a wide variety of support for PS2 disassembly & decompilation. |
## Index
- [Ghidra notes](https://github.com/ricolantern/pipo3-research/blob/main/docs/GhidraNotes.md)
## Task List
Points of interest I plan to go over, in order.
- [ ] (CURRENT FOCUS) Fully reverse and document the .i3d file format, opening the doors to full control over the game's 3D assets.
   - [ ] List all of Sony's games that you can _confirm_ use the .i3d format. Cross-reference each game's decomp to study how the format is pieced together.
   - [ ] Ape Escape 3 uses a generalized .i3d format, but other games made in the same engine around that timeframe split it up into .i3r (rig), i3m (motion), i3c (collision). Why is AE3 the odd one out? Is this a bug in the BMS script? Debug the BMS script since there seem to be other issues with it too.
   - [ ] Create basic model viewer UI.
   - [ ] Write foundations for i3d importer; focus on camera functionality for debugging the i3d output.
   - [ ] Parse i3d headers.
   - [ ] (Re)Design the i3d reader, keeping in mind the i3r, i3m, i3c variations (Any structure differences between the games??).
- [ ] Restore the text strings missing from the NTSC-J debug menu. They're still present in the code.
   - [ ] Figure out how to enable the debug menu (everyone is gatekeeping).
- [ ] Study the game's sound system.
   - [ ] Find out how .midi works in tandem with .hd and .bd.
   - [ ] Find out how reverb is applied to instruments. This is done at run-time.
   - [ ] Export to .wav?
   - [ ] The game can stream audio as well. Can I somehow disable .midi for the soundtrack entirely, replacing it with streams of the soundtrack release?
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
