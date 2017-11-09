# Jsonnet Support for Visual Studio Code

A simple bare-bones extension providing simple syntax highlighting
for [Jsonnet][jsonnet] files (specifically, files with the `.jsonnet`
and `.libsonnet` suffixes), as well as a Markdown-style preview pane
that auto-updates every time you save.

![Jsonnet preview][jsonnet-demo]

## Usage

Syntax highlighting works out of the box. Just open any `.jsonnet` or
`.libsonnet` file, and it will magically work.

To enable the Jsonnet preview pane, it is necessary to install the
Jsonnet command line tool (_e.g._, through `brew install jsonnet`). If
you don't add the `jsonnet` executable to the `PATH` then you will
need to customize `jsonnet.executablePath` in your `settings.json`, so
that the extension knows where to find it.

After this, you can use the keybinding for `jsonnet.previewToSide` (by
default this is `shift+ctrl+i`, or `shift+cmd+i` on macOS), and the
preview pane will open as in the picture above.

## Support for external variables and top-level arguments

You can define custom external variables and top-level arguments in the header
of your jsonnet file to be used in render previews. It's handy in case if
compile the file with some externally defined variables or tla but still want to
use the preview functionality.

The syntax for them is as follows:

`//e key: some value` defines external variable `key` with value `some value`

`//E key: {a: 1}` defines external variable `key` with jsonnet code of `{a: 1}`

`//t arg: test` defines top-level argument `arg` with value `test`

`//T key: {a: 1}` defines top-level argument `key` with jsonnet code of `{a: 1}`

## Customization

This extension exposes the following settings, which can be cusomized
in `settings.json`:

* `jsonnet.executablePath`: Tells the extension where to find the
  `jsonnet` executable, if it's not on the `PATH`. (NOTE: This setting
  is always necessary on Windows.)

This extension exposes the following commands, which can be bound to
keys:

* `jsonnet.previewToSide`: Compiles the Jsonnet file to JSON, places
  result in a "preview" window in the pane to the right of the active
  pane, or in the current pane if active window is pane 3 (since
  vscode only allows 3 panes). Default: bound to `shift+ctrl+i` (or
  `shift+cmd+i` on macOS).
* `jsonnet.previewToSide`: Compiles the Jsonnet file to JSON, places
  result in a "preview" window in the current active pane. Default: no
  keybinding.
* `jsonnet.extStrs`: An object of variable, value pairs. Allows you to
  customize the external variables passed to the `jsonnet` command
  line. It can be particularly useful to set this in a workspace
  configuration, so that you can set different variables on a
  per-project basis.
* `jsonnet.outputFormat`: A choice of two string literals: `["json",
  "yaml"]`. This tells the extension what format you'd like the output
  to be (_i.e._, allows you to either output JSON or YAML).

[jsonnet]: http://jsonnet.org/ "Jsonnet"
[jsonnet-demo]: https://raw.githubusercontent.com/heptio/vscode-jsonnet/master/images/kube-demo.gif
