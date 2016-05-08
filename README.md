# ppx_bitstring

PPX plugin for the OCAML OPAM bitstring package.

## Overview

This repository is a development playground. It aims at eventually being a drop-in replacement of the `ocamlp4` extension.

## Usage

The PPX extension is called `ppx_bitstring.ext`. It should be used as follows:

```bash
$ opam pin add -k git ppx_bitstring https://github.com/xguerin/ppx_bitstring
$ ocamlfind ocamlopt -linkpkg -thread -package bitstring,ppx_bitstring.ext main.ml -o main.native
```

## Syntax

Usage example with the `match` PPX extension:

```ocaml
match%bitstring bs with
| {|
    1 : 1;
    a : 2;
    b : 16 : bigendian;
    ...
  |} -> (* Do something *)
| {| _ |} -> (* Do something else *)
```

Usage example with the `let` PPX extension:

```ocaml
let%bitstring bs = {|
    1 : 1;
    a : 2;
    b : 16 : bigendian;
    ...
  |} in (* Do something here *)
```

The format of the cases being the same as the original `bitstring`, please refer to its [documentation](http://people.redhat.com/~rjones/bitstring/html/Bitstring.html).

## Contribute

To see the parse tree of a ML file:

```bash
ocamlc -dparsetree foo.ml
```

To see the output of a development version of the extension:

```bash
ocamlfind opt -package bitstring -thread -dsource -ppx ./ppx_bitstring.ext foo.ml
```

## License

Copyright (c) 2016 Xavier R. Guérin <copyright@applepine.org>

Permission to use, copy, modify, and distribute this software for any purpose with or without fee is hereby granted, provided that the above copyright notice and this permission notice appear in all copies.

THE SOFTWARE IS PROVIDED "AS IS" AND THE AUTHOR DISCLAIMS ALL WARRANTIES WITH REGARD TO THIS SOFTWARE INCLUDING ALL IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR ANY SPECIAL, DIRECT, INDIRECT, OR CONSEQUENTIAL DAMAGES OR ANY DAMAGES WHATSOEVER RESULTING FROM LOSS OF USE, DATA OR PROFITS, WHETHER IN AN ACTION OF CONTRACT, NEGLIGENCE OR OTHER TORTIOUS ACTION, ARISING OUT OF OR IN CONNECTION WITH THE USE OR PERFORMANCE OF THIS SOFTWARE.

