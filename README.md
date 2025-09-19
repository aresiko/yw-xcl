# yw-xcl
A W.I.P reader (converts -> .obj) for Yo-kai Watch XCL (X CoLlision/X Collision Layout) files used in Yo-kai Watch Blasters onwards, made in HTML. Download the `index.html` and open it with a web browser or go to [the website](https://n123git.github.io/yw-xcl). Random fact: an XCL cannot be larger than 536,870,911 bytes (~1/2GB) decompressed.

### Suppported Games
* Yo-kai Watch 3
* Yo-kai Watch Busters 2

### Untested
* Yo-kai Watch Blasters
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
  * Header (`0x00`-`0x5F`)
    * `0x00` (uint32): Main Metadata (Version num?) - usually `0x00000001`.
    * `0x08` (uint32):  Offset to the start of the vertice block?, starting from AFTER the header (so the offset given is the actual offset - `0x60`). This is usually just `0x00000000`.
    * `0x0C` (uint32): Offset to the start of the main triangle (not vertices!) block; this is also starting from AFTER the header (so the offset given is the actual offset - `0x60`).
    * `0x14` (uint32): Offset to the end of the main triangle block, relative to the start of the vertex block.
    * Any offsets not described here are because they're purpose is currently unknown! I will work on expanding this as time passess but 96 bytes is alot for this!
  * Vertex Array (Vertice Block)
    * Location is usually `0x60` onwards. But the actual location depends - read the header section for more info.
    * Each vertex consists of **3 consecutive 32-bit floats** (`x, y, z`) for its position in 3D space.
  * Triangle Array (Main Triangle Block)
    * Location: Depends; look at the header section for more info.
    * Triangle size: 6 bytes per triangle - each triangle is composed of 3 consecutive verticie indexs (uint16)


--- 

## License

* MIT License (credit isnt fully required aslong as you dont make it falsely appear as if the work was yours, implicitly or explicitly lol).
