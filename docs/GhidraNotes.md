# Ghidra Notes
Areas of interest for further research.
Contents are technical and in the context of Ghidra.

## _Game SDK Version strings_
Defined Strings search on "PSII" reveals a handful of strings that detail the exact version of some of the SDK libraries the game uses for interacting with the hardware.
This information might also give us somewhat of an estimation as to which development kits were used in development, and perhaps even help in narrowing down early builds of the game??

Information about these libraries seems to be scarce to come by, and it should also be noted that your web searches may be confused with the community-driven PS2SDK project.
Care has been taken to ensure the information below is drawn from either official PS2 documentation archives, or otherwise inferred from the decompilation.
| Location | String Representation | Library Meaning | Library Description |
| --- | --- | --- | --- |
| 00678740 | "PsIIlibcdvd 3000" | PS2 CD/DVD Library | No official docs available. Suggested to be CD/DVD interactivity due to 006fe9f0 mentioning a function `CdDiskReady`. |
| 0067c4f0 | "PsIIlibpad2 3020" | PS2 (Controller) Pad Library 2 | Interacting with the DualShock controller(s). It's predecessing library documentation can be found [here](https://archive.org/details/ps-2-programmer-tool-runtime-library-controller-library). I'm unable to find an archive for libpad2. |
| 0067c560 | "PsIIlibdbc  3020" | PS2 Debug Channel Library | Defined Strings search on "dbc" reveals several output strings mentioning sockets and RPC. The string "sceDbcGetDeviceStatus: rpc error" suggests this was probably used to communicate with a dev kit. |
| 0067c578 | "PsIIspu2mem 3000" | PS2 SPU I/O | Used for memory transfers related to sound, as suggested by 006f10b0 (`static void SoundSys::load2spu(const char*, unsigned int)`) |
| 0067f9b0 | "PsIIlibkernl3000" | PS2 Kernel Library | Self explanatory. Used for interactions with the PS2 kernel. |

TODO: Look into the specifics of the .irx files.
