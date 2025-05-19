# Essential Vim Commands

Vim is a highly efficient, open-source text editor, first released in 1991, known for its modal interface and keyboard-driven workflow ([KeyCDN Vim Commands](https://www.keycdn.com/blog/vim-commands)). It allows users to edit text in different modes—Normal, Insert, Visual, and Command-Line—making it ideal for developers and power users. This guide organizes essential Vim commands into categories, provides customization tips, and includes plugin recommendations to transform Vim into an IDE-like environment. It’s designed for users familiar with basic commands like `i`, `:wq`, and `:q!`, aiming to expand their proficiency.

## Understanding Vim Modes

Vim’s modal design is its core strength:
- **Normal Mode**: Default for navigation and commands (return with `Esc`).
- **Insert Mode**: For text editing (enter with `i`, `a`, etc.).
- **Visual Mode**: For selecting text (enter with `v`, `V`, or `Ctrl-v`).
- **Command-Line Mode**: For executing commands like saving or quitting (enter with `:`).

Mastering mode transitions is key to efficient Vim usage.

## Entering and Exiting Modes

| Command   | Description                                      |
|-----------|--------------------------------------------------|
| `i`       | Insert before the cursor.                        |
| `I`       | Insert at the start of the line.                 |
| `a`       | Append (insert after the cursor).                |
| `A`       | Append at the end of the line.                   |
| `o`       | Open a new line below and enter insert mode.     |
| `O`       | Open a new line above and enter insert mode.     |
| `Esc`     | Return to Normal mode.                           |
| `v`       | Enter Visual mode (character-wise selection).    |
| `V`       | Enter Visual mode (line-wise selection).         |
| `Ctrl-v`  | Enter Visual block mode (column selection).      |

## Saving and Quitting

| Command         | Description                                      |
|-----------------|--------------------------------------------------|
| `:w`            | Save (write) the file.                           |
| `:w <filename>` | Save as a new file.                              |
| `:wq` or `:x` or `ZZ` | Save and quit.                             |
| `:q`            | Quit (only if no unsaved changes).               |
| `:q!`           | Quit without saving (discard changes).           |
| `:qa`           | Quit all open files/buffers.                     |
| `:wqa`          | Save and quit all open files/buffers.            |

## Navigation

### Basic Movement

| Command | Description                                      |
|---------|--------------------------------------------------|
| `h`     | Move left.                                       |
| `j`     | Move down.                                       |
| `k`     | Move up.                                         |
| `l`     | Move right.                                      |

### Word Movement

| Command | Description                                      |
|---------|--------------------------------------------------|
| `w`     | Move to start of next word.                      |
| `b`     | Move to start of previous word.                  |
| `e`     | Move to end of current/next word.                |

### Line Movement

| Command | Description                                      |
|---------|--------------------------------------------------|
| `0`     | Move to start of line.                           |
| `$`     | Move to end of line.                             |
| `^`     | Move to first non-blank character of line.       |

### Screen/Document Movement

| Command     | Description                                      |
|-------------|--------------------------------------------------|
| `gg`        | Go to first line of file.                        |
| `G`         | Go to last line of file.                         |
| `<number>G` | Go to specific line (e.g., `10G` for line 10).   |
| `Ctrl-u`    | Scroll up half a screen.                         |
| `Ctrl-d`    | Scroll down half a screen.                       |
| `Ctrl-f`    | Scroll forward one screen.                       |
| `Ctrl-b`    | Scroll backward one screen.                      |

### Jumping

| Command   | Description                                      |
|-----------|--------------------------------------------------|
| `%`       | Jump to matching parenthesis, bracket, or brace. |
| `[[` or `]]` | Jump to previous/next section (useful in code). |

## Editing

| Command       | Description                                      |
|---------------|--------------------------------------------------|
| `x`           | Delete character under cursor.                   |
| `dd`          | Delete (cut) current line.                       |
| `<number>dd`  | Delete multiple lines (e.g., `3dd` deletes 3).   |
| `dw`          | Delete from cursor to end of word.               |
| `d$`          | Delete from cursor to end of line.               |
| `D`           | Same as `d$`.                                    |
| `c`           | Change (delete and enter insert mode, e.g., `cw`). |
| `r`           | Replace character under cursor.                  |
| `R`           | Enter replace mode (overwrite text).             |
| `u`           | Undo last change.                                |
| `Ctrl-r`      | Redo.                                            |
| `.`           | Repeat last change.                              |
| `yy`          | Yank (copy) current line.                        |
| `<number>yy`  | Yank multiple lines (e.g., `3yy` copies 3).      |
| `yw`          | Yank a word.                                     |
| `p`           | Paste after cursor.                              |
| `P`           | Paste before cursor.                             |

## Search and Replace

| Command             | Description                                      |
|---------------------|--------------------------------------------------|
| `/<pattern>`        | Search forward for pattern (press Enter).        |
| `?<pattern>`        | Search backward for pattern.                     |
| `n`                 | Move to next search match.                       |
| `N`                 | Move to previous search match.                   |
| `*`                 | Search forward for word under cursor.            |
| `#`                 | Search backward for word under cursor.           |
| `:%s/old/new/g`     | Replace all "old" with "new" in file.            |
| `:%s/old/new/gc`    | Replace with confirmation for each occurrence.   |

## Visual Mode Commands

| Command   | Description                                      |
|-----------|--------------------------------------------------|
| `v`       | Select text character by character.              |
| `V`       | Select entire lines.                             |
| `Ctrl-v`  | Select block (useful for columnar editing).      |

After selecting:
- `d`: Delete selected text.
- `y`: Yank (copy) selected text.
- `c`: Change selected text (delete and enter insert mode).
- `s`: Replace selected text.

## Working with Files and Buffers

| Command           | Description                                      |
|-------------------|--------------------------------------------------|
| `:e <filename>`   | Open new file for editing.                       |
| `:ls`             | List open buffers.                               |
| `:b <number>`     | Switch to specific buffer (e.g., `:b2`).         |
| `:bn`             | Go to next buffer.                               |
| `:bp`             | Go to previous buffer.                           |
| `:bd`             | Delete (close) current buffer.                   |
| `:sp <filename>`  | Split window horizontally and open file.         |
| `:vsp <filename>` | Split window vertically and open file.           |
| `Ctrl-w w`        | Switch between split windows.                    |
| `:tabnew <filename>` | Open file in new tab.                         |
| `:tabn`           | Go to next tab.                                  |
| `:tabp`           | Go to previous tab.                              |

## Advanced Commands for IDE-Like Usage

### Code Navigation

| Command | Description                                      |
|---------|--------------------------------------------------|
| `gf`    | Go to file under cursor (e.g., imports).         |
| `gd`    | Go to definition (requires ctags plugin).        |
| `]d`    | Go to next diagnostic (with linter plugin).      |
| `[d`    | Go to previous diagnostic.                       |

### Folding (Code Organization)

| Command | Description                                      |
|---------|--------------------------------------------------|
| `za`    | Toggle a fold.                                   |
| `zR`    | Open all folds.                                  |
| `zM`    | Close all folds.                                 |

### Command Execution

| Command       | Description                                      |
|---------------|--------------------------------------------------|
| `:!<command>` | Run shell command (e.g., `:!ls`).                |
| `:make`       | Run make command (for compiling).                |
| `:sh`         | Open shell within Vim (exit with `exit`).        |

### Registers and Macros

| Command       | Description                                      |
|---------------|--------------------------------------------------|
| `"<letter>y`  | Yank to specific register (e.g., `"ay`).         |
| `"<letter>p`  | Paste from specific register (e.g., `"ap`).      |
| `q<letter>`   | Start recording macro (e.g., `qa`).              |
| `q`           | Stop recording.                                  |
| `@<letter>`   | Replay macro (e.g., `@a`).                       |
| `@@`          | Replay last macro.                               |

## Customization and Plugins

Vim’s flexibility allows customization via the `~/.vimrc` file and plugins to enhance functionality.

### Configuration Commands

| Command         | Description                                      |
|-----------------|--------------------------------------------------|
| `:set <option>` | Set an option (e.g., `:set number`).             |
| `:set no<option>` | Disable an option (e.g., `:set nonumber`).     |

Common options:
- `:set number`: Show line numbers.
- `:set relativenumber`: Show relative line numbers.
- `:set autoindent`: Enable auto-indentation.
- `:set tabstop=4`: Set tab width to 4 spaces.
- `:set shiftwidth=4`: Set indentation width.
- `:set expandtab`: Use spaces instead of tabs.
- `:set ignorecase`: Ignore case in searches.
- `:set smartcase`: Case-sensitive search if uppercase used.

### Recommended Plugins

Use a plugin manager like Vim-Plug ([Vim Awesome](https://vimawesome.com/)). Install by adding to `~/.vimrc` and running `:PlugInstall`. Recommended plugins:

| Plugin        | Description                                      | Key Command                                      |
|---------------|--------------------------------------------------|--------------------------------------------------|
| NERDTree      | File explorer.                                   | `:NERDTreeToggle`                                |
| fzf.vim       | Fuzzy file finder.                               | `:Files`, `:Rg`                                  |
| ale           | Asynchronous linting.                            | `:ALENext`, `:ALEPrevious`                       |
| vim-surround  | Easy surround editing.                           | `cs"'` (change `"` to `'`)                       |
| coc.nvim      | IntelliSense for autocompletion.                 | `:CocInstall coc-pyright` (for Python)           |
| ctags/gutentags | Tag navigation for code.                       | `:tag <symbol>`                                  |
| vim-fugitive  | Git integration.                                 | `:Gstatus`, `:Gcommit`                           |

Sample `~/.vimrc`:

```vim
set number relativenumber
set autoindent
set tabstop=4 shiftwidth=4 expandtab
set ignorecase smartcase
call plug#begin('~/.vim/plugged')
Plug 'preservim/nerdtree'
Plug 'junegunn/fzf.vim'
Plug 'dense-analysis/ale'
Plug 'tpope/vim-surround'
call plug#end()
```

## Miscellaneous Tips

- **Help System**: Use `:h <topic>` for details (e.g., `:h :w` for save command).
- **Repeat Commands**: Prefix with a number (e.g., `5j` moves down 5 lines).
- **Split Windows**: Use `:sp` or `:vsp` with `Ctrl-w` for multitasking.
- **Practice**: Run `vimtutor` in terminal for interactive learning.
- **Cheat Sheet**: Keep a reference like [Vim Cheat Sheet](https://vim.rtorr.com/) handy.

## Example Workflow

1. Open a file: `vim code.py`
2. Navigate to line 10: `10G`
3. Insert text: `i`, type, then `Esc`
4. Search for a variable: `/my_var<Enter>`, move with `n`
5. Replace text: `:%s/old/new/g`
6. Save and quit: `:wq`
7. Run a command: `:!python code.py`

## Further Resources

- [Vim Cheat Sheet](https://vim.rtorr.com/): Comprehensive command reference.
- [Vim Commands Cheat Sheet](https://devhints.io/vim): Concise one-page guide.
- [A Great Vim Cheat Sheet](https://vimsheet.com/): Essential commands and configuration tips.