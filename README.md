# CFF opcode test fonts

This repository contains minimal OTF fonts intended for testing [CFF](https://www.microsoft.com/typography/otspec180/cffspec.htm) opcode support, using Type2 charstring operators as defined in [Adobe Tech Note 5177](https://www.microsoft.com/typography/otspec160/charstr2.htm).

The naming format is `cff` . `<opcode>` . `(<optional dependencies>)` . `otf`.

Currently all these fonts are "good" fonts, i.e. no intentionally bad charstrings
have been included. This may change in the future, although if you want to submit
your own fonts in a PR, please note whether it's a good or a bad font.

All fonts encode a 700 x 700  rectangle for the letter `"a"` (as well as several
others) that, after evaluating all operators, corresponds to the following charstring:

```postscript
   0    0  rmoveto
   0  700  rlineto
 700    0  rlineto
   0 -700  rlineto
-700    0  rlineto
```

If, after interpreting, the glyph does not match a 700x700 font unit rectangle 
starting at (0,0) and traced clockwise, whatever did the decoding does not
properly support the relevant CFF opcodes.

**Note:** these fonts assume the `subr` and `gsubr` opcodes are already supported.

## The 'random' opcode font

The one font that can't be tested this way is the test font for the `random` instruction,
which by its very nature cannot produce deterministic results without also fixing the
PRNG seed value, which has to be done outside of the font itself and will lead to
different randomness pattern based on the PRNG algorith, used. As such, the following
outline is used for the `random` opcode font, and consequently the glyph outline 
should be tested based on whether "the next vertex" is within the expected zero to one
font unit deviation.

```postscript
       0    0  rmoveto
  random  700  rlineto
  700  random  rlineto
  random -700  rlineto
 -700  random  rlineto
```

## Tools used

I use https://github.com/pomax/simple-CFF-builder for building these fonts, which uses http://pomax.github.io/node-type2-charstring/ (the library, not the site) to specifically convert type2 instructions into CFF charstring bytes.

## License information

There is no code in this repo, and so there is no LICENSE file: individual fonts already come with their own license information embedded so that should be good enough. Each font has a `name` table in which the data is explicitly marked as "copyright free", "trademark free" and "license free". These fonts are in the public domain and you can use them however you want.
