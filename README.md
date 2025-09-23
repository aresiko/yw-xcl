# yw-xcl
A W.I.P reader (converts -> .obj) for Yo-kai Watch XCL (X CoLlision/X Collision Layout) files used in Yo-kai Watch Blasters onwards, made in HTML. Download the `index.html` and open it with a web browser or go to [the website](https://n123git.github.io/yw-xcl). Random fact: an XCL cannot be larger than 536,870,911 bytes (~1/2GB) decompressed.

Notes:
* The XCL Parser currently has a minor bug:
  * For a small number of XCLs one or two triangles wont be picked up - this is currently being worked on!

### Suppported Games
* Yo-kai Watch 3
* Yo-kai Watch Busters 2
* Yo-kai Watch Blasters

### Untested
* Snack World

  ## XCL Specification
  The purpose of the file format is listed above - it is used *exclusively for maps* and has no signature/magic.
  The bytes take the following format:
  
  ### Compressed XCL
  * 4 byte header:
     * bits 0-2: compression method - same as in other level5 formats i.e. (0=raw, 1=LZSS, ...)
       * `0` = Raw (uncompressed)
       * `1` = LZSS compressed
       * `2` = Huffman (8-bit table) \[unsupported in this reader]
       * `3` = Huffman (4-bit table) \[unsupported]
       * `4` = RLE \[unsupported]
       * `5` = zlib\_level5 \[unsupported]
     * bits 3-31: size of the decompressed file.
  * The rest is the compressed payload - nothing special lol :P
  Support for other compression types will roll out next update (hopefully)
  ### Decompressed XCL
  * Header (`0x00`-`0x5F`)? - size unconfirmed for now.
    * `0x00` (uint32): Main Metadata (Version num?) - usually `0x00000001` or `0x00000100`.
    * `0x08` (uint32):  Offset to the start of the vertice block.
    * `0x0C` (uint32): Offset to the start of the main triangle (not vertices!) block; this is also starting from AFTER the header (so the offset given is the actual offset - `0x60`).
    * `0x4C` (uint32): Usually (for smaller maps) this stores the length (in bytes) of the vertex array. Sometimes this is `00 00 00 00`; in that case the below offset stores it.
    * `0x58` (uint32): Stores the length (in bytes) of the vertex array when `0x4C` is `00 00 00 00`.
    * <!-- `0x14` (uint32): Offset -->
  * Vertex Array (Vertice Block)
    * Location is usually `0xC0` or `0xA4` onwards. But the actual location is stored in the header - read the header section for more info.
    * Each vertex consists of **3 consecutive 32-bit floats** (`x, y, z`) for its position in 3D space.
  * Triangle Array (Main Triangle Block)
    * Location: Depends; look at the header section for more info.
    * Triangle size: 6 bytes per triangle - each triangle is composed of 3 consecutive verticie indexs (uint16)


--- 

## License

* MIT License (I dont really need credit aslong as you dont implicitly or explicitly take credit for work that isnt yours >>:( ).
