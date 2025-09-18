# yw-xcl
A W.I.P reader for Yo-kai Watch XCL (X Collision) files used in Yo-kai Watch Blasters onwards made in HTML.

## XCL Specification
The purpose of the file format is listed above - it is used *eclusively for maps* and has no signature/magic.
The bytes take the following format:
* 4 byte header:
   * bits 0-2: compression method - same as in other level5 formats i.e. (0=raw, 1=LZSS, ...)
   * bits 3-31: size of the decompressed file
