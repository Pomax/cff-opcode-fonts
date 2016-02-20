# CFF opcode test fonts

This repository contains minimal OTF fonts intended for testing CFF opcode support.

The naming format is `cff` . `opcode` . `(optional dependencies)` . `otf`.

Currently all these fonts are "good" fonts, i.e. no intentionally bad charstrings
have been included. This may change in the future, although if you want to submit
your own fonts in a PR, please note whether it's a good or a bad font.

All fonts encode a 700 x 700  rectangle. If, after rendering, the glyph does not
match a `(0,0)`, `(0,700)`, `(700,700)`, `(700,0)` rectangle, measured in font units,
whatever did the decoding does not properly support the relevant CFF opcodes.
