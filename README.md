# Bash Language Server

Bash language server implementation based on [Tree Sitter][tree-sitter] and its [grammar for Bash][tree-sitter-bash]
with [explainshell][explainshell] integration.

## Features

- [x] Jump to declaration
- [x] Find references
- [x] Code Outline & Show Symbols
- [x] Highlight occurrences
- [x] Code completion
- [x] Simple diagnostics reporting
- [x] Documentation for flags on hover
- [ ] Rename symbol

## Installation

```bash
npm i -g bash-language-server
```

If you encounter `EACCESS` errors on installation, similarly to what's described in [#93](https://github.com/mads-hartmann/bash-language-server/issues/93), you may need to solve either or both of the following issues:

- https://wiki.archlinux.org/index.php/Node.js#node-gyp_python_errors
- https://bugs.archlinux.org/task/54981

The workaround for the missing `semver@5.3.0` dependency described in [the Arch Linux Bug report](https://bugs.archlinux.org/task/54981), is best workaround by running `npm install` in `/usr/lib/node_modules/node-gyp`.

### Clients

The following editors and IDEs have available clients:

- Visual Studio Code ([Bash IDE][vscode-marketplace])
- Atom ([ide-bash][ide-bash])
- Vim ([see below](#vim))
- Neovim ([see below](#neovim))
- [Oni](https://github.com/onivim/oni) ([see below](#oni))
- Eclipse ([ShellWax](https://marketplace.eclipse.org/content/shellwax))

#### Vim

For Vim 8 or later install the plugin [prabirshrestha/vim-lsp][vim-lsp] and add the following configuration to `.vimrc`:

```vim
if executable('bash-language-server')
  au User lsp_setup call lsp#register_server({
        \ 'name': 'bash-language-server',
        \ 'cmd': {server_info->[&shell, &shellcmdflag, 'bash-language-server start']},
        \ 'whitelist': ['sh'],
        \ })
endif
```

For Vim 8 or Neovim using [neoclide/coc.nvim][coc.nvim], according to [it's Wiki article](https://github.com/neoclide/coc.nvim/wiki/Language-servers#bash), add the following to your `coc-settings.json`:

```jsonc
  "languageserver": {
    "bash": {
      "command": "bash-language-server",
      "args": ["start"],
      "filetypes": ["sh"],
      "ignoredRootPaths": ["~"]
    }
  }
```

For Vim 8 or NeoVim using [w0rp/ale][vim-ale] add the following
configuration to your `.vimrc`:

```vim
let g:ale_linters = {
    \ 'sh': ['language_server'],
    \ }
```

#### Neovim

Install the plugin [autozimu/LanguageClient-neovim][languageclient-neovim] and add the following configuration to
`init.vim`:

```vim
let g:LanguageClient_serverCommands = {
    \ 'sh': ['bash-language-server', 'start']
    \ }
```

#### Oni

On the config file (`File -> Preferences -> Edit Oni config`) add the following configuration:

```javascript
"language.bash.languageServer.command": "bash-language-server",
"language.bash.languageServer.arguments": ["start"],
```

## Development Guide

Please see [docs/development-guide][dev-guide] for more information.

[tree-sitter]: https://github.com/tree-sitter/tree-sitter
[tree-sitter-bash]: https://github.com/tree-sitter/tree-sitter-bash
[vscode-marketplace]: https://marketplace.visualstudio.com/items?itemName=mads-hartmann.bash-ide-vscode
[dev-guide]: https://github.com/mads-hartmann/bash-language-server/blob/master/docs/development-guide.md
[ide-bash]: https://atom.io/packages/ide-bash
[explainshell]: https://explainshell.com/
[languageclient-neovim]: https://github.com/autozimu/LanguageClient-neovim
[vim-lsp]: https://github.com/prabirshrestha/vim-lsp
[vim-ale]: https://github.com/w0rp/ale
[coc.nvim]: https://github.com/neoclide/coc.nvim
