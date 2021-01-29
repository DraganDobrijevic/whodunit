# Questions

## What's `stdint.h`?
stdint.h is a header file in the C standard library introduced in the C99 standard library to allow programmers to write more portable code by providing a set of typedefs that specify exact-width integer types, together with the defined minimum and maximum allowable values for each type, using macros. 
stdint.h a header file that provides access to several functions related to integer standards, such as uint8_t, uint32_t, int32_t, and uint16_t. These functions specify the exact width of integers and allow code to be more portable by setting widths dependent on the processor targets (whether 32 bit or 64 bit, for example).

## What's the point of using `uint8_t`, `uint32_t`, `int32_t`, and `uint16_t` in a program?
It's very useful when you do computations on bits, or on specific range of values (in cryptography, or image processing for example) because you don't have to "detect" the size of a long, or an unsigned int, you just "use" what you need. If you want 8 unsigned bits, use uint8_t like you did.
And I insist on the fact that it's cross-platform, you can compile your program on a 64-bits Linux and a 32-bits Windows, and you won't have to change the types.
uint8_t is an unsigned (u) int (integer) of 8 bits, uint32_t is an unsigned integer of 32 bits, int32_t is a signed integer, and a uint16_t is an unsigned 16 bit integer. The number refers to the number of bits it can allocate. You can TYPEDEF them into more common terms like byte, long, word, etc

## How many bytes is a `BYTE`, a `DWORD`, a `LONG`, and a `WORD`, respectively?
BYTE: 1,  DWORD: 4,   LONG: 4,   WORD: 2

## What (in ASCII, decimal, or hexadecimal) must the first two bytes of any BMP file be? Leading bytes used to identify file formats (with high probability) are generally called "magic numbers."
The first two bytes: BM, or the hex 0x4D42

## What's the difference between `bfSize` and `biSize`?
bfSize is the size, in bytes, of a bitmap file (246 bytes for smiley.bmp). 
biSize specifies the number of bytes required by the structure BITMAPINFOHEADER.

## What does it mean if `biHeight` is negative?
If biHeight is negative, the bitmap is a top-down DIB and its origin is the upper-left corner.
If biHeight is negative, indicating a top-down DIB, biCompression must be either BI_RGB or BI_BITFIELDS. Top-down DIBs cannot be compressed 

## What field in `BITMAPINFOHEADER` specifies the BMP's color depth (i.e., bits per pixel)?
The biBitCount specifies the number of bits per pixel.

## Why might `fopen` return `NULL` in `copy.c`?

fopen will return null if it cannot open the file. This can happen if there is not enough memory or the file cannot be found.
If it can't find the file, it will.
   - There may be a few reasons why fopen would return NULL in line 37 of copy.c. Since the program reaches line 37, there
    seems to be 2 command-line arguments, and since you are writing to a file in line 37, if the file doesn't already exist
    the program will create the file and store it in the current working directory. If the computer cannot
    allocate enough memory to create the desired file, NULL would be returned. Also, there may be a permissions error when
    trying to write to an open file, or you may not have access to that file.

## Why is the third argument to `fread` always `1` in our code?
The third argument determines the number of elements fread will read. This argument is always 1 in our code because we are always reading one element.

## What value does `copy.c` assign to `padding` if `bi.biWidth` is `3`?
int padding = (4 - (bi.biWidth * sizeof(RGBTRIPLE)) % 4) % 4;
RGBTRIPLE = 3, and 3 * 3 = 9 --> 9 % 4 = 1 --> 4 - 1 = 3 --> 3 % 4 = 3.
int padding = (4 - (3 * 3 % 4) % 4;
int padding = 3;

## What does `fseek` do?
fseek moves the file position indicator.
It moves to a specific location in a file.
fseek(inptr, amount, from);
inptr: FILE* to seek in
amount: number of bytes to move cursor  --> amount is padding in whodunit.c and copy.c
from: SEEK_CUR (current position in file) --> in whodunit.c and copy.c we use SEEK_CUR
      SEEK_SET (beginning of file)
      SEEK_END (end of file)
In copy.c and whodunit.c's case, it skips over the padding int and
looks for next RGBTRIPLE to read.

## What is `SEEK_CUR`?
SEEK_CUR (current position in file) --> In whodunit.c and copy.c we use SEEK_CUR
SEEK_CUR is an option used in fseek to set the offset relative to the current pointer position.

