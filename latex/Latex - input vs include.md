---
date: 2023-12-13
tags:
  - latex
---
**`\input{filename}`** imports the commands from `filename.tex` into the target file; it's equivalent to typing all the commands from `filename.tex` right into the current file where the `\input` line is.

**`\include{filename}`** essentially does a `\clearpage` before and after `\input{filename}`, together with some magic to switch to another `.aux` file, and omits the inclusion at all if you have an `\includeonly` without the filename in the argument. This is primarily useful when you have a big project on a slow computer; changing one of the include targets won't force you to regenerate the outputs of all the rest.

`\include{filename}` gets you the speed bonus, but it also can't be nested, can't appear in the preamble, and forces page breaks around the included text.
