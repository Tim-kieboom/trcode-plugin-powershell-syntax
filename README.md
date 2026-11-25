# PowerShell syntax for TerminalCode

Syntax highlighting for PowerShell (`.ps1`, `.psm1`, `.psd1`) as a [TerminalCode](https://github.com/Tim-kieboom/TerminalCode) plugin.

It is a language and nothing else: there is no code in it and no pane. The plugin is

- `powershell.wasm`, the tree-sitter grammar built for WebAssembly,
- `manifest.toml`, which says which files are PowerShell (`[language]`: `extensions`, `comment`) and has the
  highlight query as text.

TerminalCode loads the grammar in its sandbox (plugin API 1.12, TerminalCode 0.11.0 or later) and colors the
files with the query, using the colors of your theme (`syntax.keyword`, `syntax.string`, ... in the theme file).

## Use

"Plugins: Manage", install **PowerShell**, and turn it on. PowerShell files are colored when they are opened, and `ctrl+/` comments a line with `#`.

## Where the grammar comes from

The grammar and the query are those of [airbus-cert/tree-sitter-powershell](https://github.com/airbus-cert/tree-sitter-powershell) at v0.26.6 (65ea691)
(MIT, `LICENSE-GRAMMAR`). The module was built from that revision with the tree-sitter CLI:

```sh
git clone https://github.com/airbus-cert/tree-sitter-powershell && cd tree-sitter-powershell
git checkout v0.26.6
tree-sitter build --wasm -o powershell.wasm
```

A new version of the grammar needs a new `version` in `manifest.toml` and a release (the module is the file the
installer checks). The query is copied into the manifest with its patterns in the opposite order (TerminalCode takes the first of two patterns on the same text; the grammar's file is written for the last).

## Licence

The plugin is MIT or Apache-2.0, as the other plugins; the grammar is MIT (`LICENSE-GRAMMAR`).
