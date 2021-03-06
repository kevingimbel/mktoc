# `mktoc`
> Markdown Table of Content generator

![](https://github.com/kevingimbel/mktoc/workflows/Clippy%20check/badge.svg)

<!-- BEGIN mktoc -->
- [About](#about)
- [Installation](#installation)
  - [Cargo](#cargo)
  - [Binary](#binary)
- [Usage](#usage)
  - [Update Markdown file](#update-markdown-file)
  - [Command line](#command-line)
  - [Environment configuration](#environment-configuration)
- [Auto-run with VSCode](#auto-run-with-vscode)
- [Performance](#performance)
- [License](#license)
<!-- END mktoc -->

## About

`mktoc` parses markdown files and generates a Table Of Content linking all headlines up to heading level 6 deep, or as specified by command line arguments. A start depth and maximum depth can be specified.

## Installation

`mktoc` can be installed using Cargo, the Rust package manager.

### Cargo

```sh
$ cargo install mktoc
```
#### Update

```
$ cargo install --force mktoc
```

### Binary

Binaries are actually not available yet. If you know how releasing binaries with Rust can be implemented, please let me know!

## Usage

### Update Markdown file

Add the following HTML comment into the Markdown file where the Table of Contents should be rendered.

```
<!-- BEGIN mktoc -->
<!-- END mktoc -->
```

Everything between those comments will be replaced!

### Command line

Specify `--stdout` or `-s` to output generated content to `stdout` instead of overwriting file. By default the specified file will be overwritten.

```
# mktoc [FLAGS] [OPTIONS] [file] 
$ mktoc -s README.md
$ mktoc -m 2 -M 4 README.md
$ mktoc
```
If no arguments are given the default or configured (via environment) values are
used. 

See `mktoc --help` for list of all arguments and flags.

```
mktoc

USAGE:
mktoc [FLAGS] [OPTIONS] [file]

FLAGS:
-h, --help       Prints help information
-s, --stdout     If set will output to stdout instead of replacing content in file
-V, --version    Prints version information

OPTIONS:
-M, --max-depth <max-depth>    Maximum heading level [env: MKTOC_MAX_DEPTH=]  [default: 6]
-m, --min-depth <min-depth>    Minimum heading level [env: MKTOC_MIN_DEPTH=2]  [default: 1]

ARGS:
<file>     [default: README.md]
```

### Environment configuration

mktoc can be configured with environment variables, namely:

- `MKTOC_MIN_DEPTH` equal to `-m`
- `MKTOC_MAX_DEPTH` equal to `-M`

Place these variables in a shell environment file such as `~/.bashrc` or
`~/.zshrc`, then just run mktoc without `-m` and `-M`

```sh
# The following in ~/.bashrc configures mktoc to render headings from level 2 to
# level 4
# 
# MKTOC_MIN_DEPTH=2
# MKTOC_MAX_DEPTH=4

$ mktoc README.md
```

## Auto-run with VSCode

For VSCode the [Run on save](https://github.com/emeraldwalk/vscode-runonsave) extension can be used to trigger mktoc.

Install the extension and then add the following config to workspace or user `settings.json`.

```json
"emeraldwalk.runonsave": {
    "commands": [
        {
            "match": "\\.md$",
            "cmd": "mktoc ${file}"
        }
    ]
}
```

This will run the command for every markdown file on safe. If there is no mktoc comment in the Markdown file nothing happens.

## Performance

`mktoc` is fast but can probably be even faster! Pull Requests and bug reports are appreciated!

## License

MIT, see LICENSE file.
