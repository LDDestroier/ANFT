# *COS 6:* Nitrogen Fingers Text

## Quick information
| Information |                           |
| ----------- | ------------------------- |
| Version     | 0.0.0                     |
| Type        | Image file format         |
| MIME        | `image/anft`              |
| Extensions  | `.anft`, `.ant`           |

## Technical details
The format is nearly identical to the “Nitrogen Fingers Text” format in that colors are defined using a hexadecimal character (0-9 and a-f), and the basic structure is mostly untouched.

However, unlike NFT, the “Animated Nitrogen Fingers Text” format stores multiple “frames”, or separate images in the same file, separated by a third special character.

| Byte | Represents |
| ---- | ---------- |
|  29  | Indicates the beginning of a frame |
|  30  | Background colour definition |
|  31  | Text colour definition |

If a 30 or 31 character is encountered, the character immediately after will be a hexadecimal character or a space (representing transparent). If the character is 30, the color represented by the hexadecimal becomes the ‘active’ background color. Hence, any following text will use that active background until the next 30 character changes it. The same applies with the 31 character, but it instead changes the text color.

At the beginning of every “frame”, the 29 character and a newline must precede the image data. Any data before the first 29 character is ignored.

### Text characters
Any character that is not `30`, `31` or the character immediately after those two represents the character that should be written to the screen. A space represents a blank (background colour only) pixel. However, if the character after `30` or `31` isn't a hexadecimal character, then that character will be written without being parsed as a special character (so you could print `29`, `30` or `31` this way.)

As with the paintutils format, each line represents a row of pixels. When the line ends 'active' background and text colours are reset, with the default being transparent.

### Example
In this example, the 29 character is represented by ~, the 30 character by @, the 31 character represented by #, and the space character by .
```
~
@4a@3#bnft
@3Fr@d1.
@d….
~
@4a@3#bnft
@3Fr@d2.
@d….
```

Creates

[IMAGE REPRESENTING FRAME 1]

and

[IMAGE EPRESENTING FRAME 2]



















