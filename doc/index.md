Welcome to myst's documentation!
================================

A little site to test out the Myst Sphinx parser. This will probably uncover
some bugs, so please report them [here](https://github.com/ExecutableBookProject/meta/issues/24)
if you find any more.

## Installing the Myst parser

Installation instructions can be found in the
[`myst_parser` README](https://github.com/ExecutableBookProject/myst_parser#myst_parser)

```console
pip install -e git+https://github.com/ExecutableBookProject/myst_parser.git#egg=myst_parser[sphinx,code_style,testing]
```

This should install the myst fork of mistletoe, along with the Sphinx parser
that is included in the "extensions" configuration of this site.

Here are the site contents:

```{toctree}
---
maxdepth: 2
caption: Contents
---
examples.md
content/wealth_dynamics.md
```

```{toctree}
---
hidden: True
---
content/heavy_tails.md
content/kesten_processes.md
```
