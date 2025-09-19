# yw-xcl
A W.I.P reader (converts -> .obj) for Yo-kai Watch XCL (X Collision) files used in Yo-kai Watch Blasters onwards made in HTML. Download the `index.html` and open it with a web browser or go to [the website](https://n123git.github.io/yw-xcl)

## XCL Specification
The purpose of the file format is listed above - it is used *exclusively for maps* and has no signature/magic.
The bytes take the following format:
* 4 byte header:
   * bits 0-2: compression method - same as in other level5 formats i.e. (0=raw, 1=LZSS, ...)
     * `0` = Raw (uncompressed)
     * `1` = LZSS compressed
     * `2` = Huffman (8-bit table) \[unsupported in this reader]
     * `3` = Huffman (4-bit table) \[unsupported]
     * `4` = RLE \[unsupported]
     * `5` = zlib\_level5 \[unsupported]
   * bits 3-31: size of the decompressed file.
Support for other compression types will roll out next update (hopefully)

* Vertex Array 
  * Located at an offset stored at **byte 8–11** of the decompressed file (little-endian 32-bit integer).
  * Each vertex consists of **3 consecutive 32-bit floats** (`x, y, z`) for its position in 3D space.


<!--### 3. Triangle Array-->

<!-- does this really exist?? * Follows the vertex array. -->
<!-- * Triangles are stored as **3 consecutive 16-bit integers** (little-endian), indexing into the vertex array. -->
<!-- * Triangles referencing vertices out of bounds are ignored. -->

--- 

## License

* MIT License (credit isnt fully required aslong as you dont make it falsely appear as if the work was yours, implicitly or explicitly lol).
