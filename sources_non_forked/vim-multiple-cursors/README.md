# vim-multiple-cursors [![Build Status](https://travis-ci.org/terryma/vim-multiple-cursors.png)](https://travis-ci.org/terryma/vim-multiple-cursors)

## About
[There](https://github.com/paradigm/vim-multicursor) [have](https://github.com/felixr/vim-multiedit) [been](https://github.com/hlissner/vim-multiedit) [many](https://github.com/adinapoli/vim-markmultiple) [attempts](https://github.com/AndrewRadev/multichange.vim) at bringing Sublime Text's awesome [multiple selection][sublime-multiple-selection] feature into Vim, but none so far have been in my opinion a faithful port that is simplistic to use, yet powerful and intuitive enough for an existing Vim user. [vim-multiple-cursors] is yet another attempt at that.

### It's great for quick refactoring
![Example1](assets/example1.gif?raw=true)

### Add a cursor to each line of your visual selection
![Example2](assets/example2.gif?raw=true)

### Do it backwards too! This is not just a replay of the above gif :)
![Example3](assets/example3.gif?raw=true)

### Add multiple cursors using regexes
![Example4](assets/example4.gif?raw=true)

To see what keystrokes are used for the above example, see [this issue](https://github.com/terryma/vim-multiple-cursors/issues/39).

## Features
- Live update in Insert mode
- One key to rule it all! See [Quick Start](#quick-start) on what the key does in different scenarios
- Works in Normal, Insert, and Visual mode for SINGLE key command

## Installation
Install using [Pathogen], [Vundle], [Neobundle], or your favorite Vim package manager.

## Quick Start
Out of the box, all you need to know is a single key `Ctrl-n`. Pressing the key in Normal mode highlights the current word under the cursor in Visual mode and places a virtual cursor at the end of it. Pressing it again finds the next ocurrence and places another virtual cursor at the end of the visual selection. If you select multiple lines in Visual mode, pressing the key puts a virtual cursor at every line and leaves you in Normal mode.

After you've marked all your locations with `Ctrl-n`, you can change the visual selection with normal Vim motion commands in Visual mode. You could go to Normal mode by pressing `v` and wield your motion commands there. Single key command to switch to Insert mode such as `c` or `s` from Visual mode or `i`, `a`, `I`, `A` in Normal mode should work without any issues.

At any time, you can press `<Esc>` to exit back to regular Vim.

Two additional keys are also mapped:
- `Ctrl-p` in Visual mode will remove the current virtual cursor and go back to the previous virtual cursor location. This is useful if you are trigger happy with `Ctrl-n` and accidentally went too far.
- `Ctrl-x` in Visual mode will remove the current virtual cursor and skip to the next virtual cursor location. This is useful if you don't want the current selection to be a candidate to operate on later.

You can also add multiple cursors using a regular expression. The command `MultipleCursorsFind` accepts a range and a pattern, and it will create a virtual cursor at the end of every match within the range. If no range is passed in, then it defaults to the entire buffer.  

**NOTE:** If at any time you have lingering cursors on screen, you can press `Ctrl-n` in Normal mode and it will remove all prior cursors before starting a new one.

## Mapping
Out of the box, only the single key `Ctrl-n` is mapped in regular Vim's Normal mode and Visual mode to provide the functionality mentioned above. `Ctrl-n`, `Ctrl-p`, `Ctrl-x`, and `<Esc>` are mapped in the special multicursor mode once you've added at least one virtual cursor to the buffer. If you don't like the plugin taking over your favorite key bindings, you can turn off the default with
```
let g:multi_cursor_use_default_mapping=0
```

You can then map the 'next', 'previous', 'skip', and 'exit' keys like the following:
```
" Default mapping
let g:multi_cursor_next_key='<C-n>'
let g:multi_cursor_prev_key='<C-p>'
let g:multi_cursor_skip_key='<C-x>'
let g:multi_cursor_quit_key='<Esc>'
```

By default, the 'next' key is also used to enter multicursor mode. If you want to use a different key to start multicursor mode than for selecting the next location, do like the following:
```
" Map start key separately from next key
let g:multi_cursor_start_key='<F6>'
```

**IMPORTANT:** Please note that currently only single keystrokes and special keys can be mapped. This contraint is also the reason why multikey commands such as `ciw` do not work and cause unexpected behavior in Normal mode. This means that a mapping like `<Leader>n` will NOT work correctly. For a list of special keys that are supported, see `help :key-notation`

**NOTE:** Please make sure to always map something to `g:multi_cursor_quit_key`, otherwise you'll have a tough time quitting from multicursor mode.

**NOTE:** Prior to version 1.3, the recommended way to map the keys is using the expressoin quote syntax in Vim, using something like `"\<C-n>"` or `"\<Esc>"` (see h: expr-quote). After 1.3, the recommended way is to use a raw string like above. If your key mappings don't appear to work, give the new syntax a try.

## Setting
Currently there're two additional global settings one can tweak:
### ```g:multi_cursor_exit_from_visual_mode``` (Default: 1)

If set to 0, then pressing `g:multi_cursor_quit_key` in _Visual_ mode will not quit and delete all existing cursors. This is useful if you want to press Escape and go back to Normal mode, and still be able to operate on all the cursors.

### ```g:multi_cursor_exit_from_insert_mode``` (Default: 1)
If set to 0, then pressing `g:multi_cursor_quit_key` in _Insert_ mode will not quit and delete all existing cursors. This is useful if you want to press Escape and go back to Normal mode, and still be able to operate on all the cursors.

### Highlight
The plugin uses the highlight group `multiple_cursors_cursor` and `multiple_cursors_visual` to highlight the virtual cursors and their visual selections respectively. You can customize them by putting something similar like the following in your vimrc:

```
" Default highlighting (see help :highlight and help :highlight-link)
highlight multiple_cursors_cursor term=reverse cterm=reverse gui=reverse
highlight link multiple_cursors_visual Visual
```

## Issues
- Multi key commands like `ciw` do not work at the moment
- All user input typed before Vim is able to fan out the last operation to all cursors is lost. This is a implementation decision to keep the input perfectly synced in all locations, at the cost of potentially losing user input.
- Select mode is not implemented

## Changelog
See [CHANGELOG.md](CHANGELOG.md)

## Contributing
As one can see, there're still many issues to be resolved, patches and suggestions are always welcome! A list of open feature requests can be found [here](../../issues?labels=enhancement&state=open).

## Credit
Obviously inspired by Sublime Text's [multiple selection][sublime-multiple-selection] feature, also encouraged by Emac's [multiple cursors][emacs-multiple-cursors] implemetation by Magnar Sveen

[vim-multiple-cursors]:http://github.com/terryma/vim-multiple-cursors
[sublime-multiple-selection]:http://www.sublimetext.com/docs/2/multiple_selection_with_the_keyboard.html
[Pathogen]:http://github.com/tpope/vim-pathogen
[Vundle]:http://github.com/gmarik/vundle
[Neobundle]:http://github.com/Shougo/neobundle.vim
[emacs-multiple-cursors]:https://github.com/magnars/multiple-cursors.el



[![Bitdeli Badge](https://d2weczhvl823v0.cloudfront.net/terryma/vim-multiple-cursors/trend.png)](https://bitdeli.com/free "Bitdeli Badge")

