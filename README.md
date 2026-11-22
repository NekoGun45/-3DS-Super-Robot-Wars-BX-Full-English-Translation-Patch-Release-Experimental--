SUPER ROBOT WARS BX - ENGLISH PATCH V0.9.3
Installation guide (xdelta patches: SRW_BX_EN_V0.9.3_xdelta.zip)
================================================================
Known emulation quirk: sometimes, after a cutscene, the screen fades to black and stays there. The game hasn't frozen or crashed; just press A once or a few times and it will continue.
(this also happens in the original japanese game when you emulate it sometimes not a bug or glitch related to any patch)

This package contains only patches. You apply them to files taken
from your own copy of the game.

Title ID of Super Robot Wars BX: 0004000000127900


WHAT YOU NEED
-------------

- A DECRYPTED dump of your own Japanese Super Robot Wars BX
  (.3ds / .cci / .cxi).
- Citra.
- xdelta3 (https://github.com/jmacd/xdelta-gpl/releases),
  or a GUI patcher such as Delta Patcher.
- Python 3 (only for the helper scripts in the "tools" folder).


STEP 1 - GET THE ORIGINAL FILES
-------------------------------

a) RomFS files:
   In Citra, right-click the game and choose "Dump RomFS".
   From the dumped folder you need these four files:
     arcTacPrmDat.bin
     arcCmnPrmDat.bin
     arcBtlPrmDat.bin
     arcBtlMsgDat.bin

b) code.bin:
   Open a terminal in the extracted patch folder and run:

     python tools/extract_code.py "your_rom.3ds"

   It creates code_original.bin next to your ROM.
   (The ROM is only read, never modified.)


STEP 2 - APPLY THE PATCHES
--------------------------

EASY WAY (recommended)

  1. Put xdelta3.exe inside the "tools" folder
     (or have xdelta3 on your PATH).
  2. Run:

       python tools/apply_patches.py <dumped_romfs_folder> <code_original.bin>

     Example:
       python tools/apply_patches.py "C:\dump\romfs" "C:\roms\code_original.bin"

  The script checks that your original files are the correct ones,
  applies every patch, checks the result, and creates a ready-to-use
  folder:

       tools\0004000000127900\

MANUAL WAY

  Apply each patch from the "patches" folder to the matching original
  file with xdelta3 or Delta Patcher:

    Original file          Patch                  Result
    arcTacPrmDat.bin   +   arcTacPrmDat.xdelta  = arcTacPrmDat.bin
    arcCmnPrmDat.bin   +   arcCmnPrmDat.xdelta  = arcCmnPrmDat.bin
    arcBtlPrmDat.bin   +   arcBtlPrmDat.xdelta  = arcBtlPrmDat.bin
    arcBtlMsgDat.bin   +   arcBtlMsgDat.xdelta  = arcBtlMsgDat.bin
    code_original.bin  +   code.xdelta          = code.bin

  Command line example:
    xdelta3 -d -s arcTacPrmDat.bin patches\arcTacPrmDat.xdelta arcTacPrmDat_patched.bin

  Then rename the results to the names in the "Result" column.


STEP 3 - INSTALL IN CITRA
-------------------------

1. Right-click the game in Citra and choose "Open Mods Location".
2. Place the patched files like this:

     ...\load\mods\0004000000127900\
       code.bin
       romfs\
         arcTacPrmDat.bin
         arcCmnPrmDat.bin
         arcBtlPrmDat.bin
         arcBtlMsgDat.bin

   (If you used apply_patches.py, just copy the contents of
   tools\0004000000127900\ there.)

3. Boot the game normally from your original, unmodified ROM.


CHECKSUMS (MD5)
---------------

File               Original                          Patched
arcTacPrmDat.bin   7093ef37be2ab87166a3e740e05b55ab  fa356266a045d213e354caccfa005176
arcCmnPrmDat.bin   3ef0458a81c311147bbe7957d69e0b74  35e84a3bed98e3c20017288ad6c36284
arcBtlPrmDat.bin   1e40a8ee87ae71f02e136383da4508be  36e1bb79ce6068804ecf807186a0d673
arcBtlMsgDat.bin   ba354eecb8747b758d069a8e2ed0556b  69ca818d91eb440a7935e4edd977aff1
code.bin           b9f2ff6be2f089e528fb28e74568e613  62809443d00497bd4c79e66fe06c1e8f

If an original file doesn't match, it doesn't come from an unmodified
Japanese ROM, and the patch won't apply correctly.


IMPORTANT
---------

- Always use the patched code.bin. The English interface and battle
  dialogue need it. Without it the game can show a black screen at
  boot or crash when a battle starts.
- If you were playing with an older test version of the patch, load
  a regular save, not a Citra save state: a save state keeps the old
  text in memory.


REAL HARDWARE (Luma3DS)
-----------------------

Tested and working on an original 2DS. Use Luma3DS's built-in LayeredFS
(Luma 7.0 or later, with "Enable game patching" turned on in Luma's config):
copy the contents of the 0004000000127900 folder to

  SD:\luma\titles\0004000000127900\

so that you end up with:

  SD:\luma\titles\0004000000127900\code.bin
  SD:\luma\titles\0004000000127900\romfs\  (the four .bin files)

If the game is installed as a CIA, make sure its seed is installed on the
console, or it won't boot.
