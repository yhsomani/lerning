# Vim Essential Commands Guide

This guide provides a comprehensive list of essential Vim commands for navigation, editing, saving, quitting, searching, and advanced tasks to help you use Vim effectively as an editor or IDE. It assumes familiarity with basic commands like `i`, `:wq`, and `:q!`.

## 1. Modes in Vim

Vim operates in different modes, each serving a specific purpose:

- **Normal Mode**: Default mode for navigation and commands (return with `Esc`).
- **Insert Mode**: For typing/editing text (entered via `i`, `a`, etc.).
- **Visual Mode**: For selecting text (entered via `v`, `V`, or `Ctrl-v`).
- **Command-Line Mode**: For executing commands like saving or quitting (entered via `:`).

## 2. Essential Commands

### Entering/Exiting Modes

- `i`: Insert before the cursor.
- `I`: Insert at the start of the line.
- `a`: Append after the cursor.
- `A`: Append at the end of the line.
- `o`: Open a new line below and enter insert mode.
- `O`: Open a new line above and enter insert mode.
- `Esc`: Return to Normal mode.
- `v`: Enter Visual mode (character-wise).
- `V`: Enter Visual mode (line-wise).
- `Ctrl-v`: Enter Visual block mode (column selection).

### Saving and Quitting

- `:w`: Save the file.
- `:w <filename>`: Save as a new file.
- `:wq` or `:x` or `ZZ`: Save and quit.
- `:q`: Quit (if no unsaved changes).
- `:q!`: Quit without saving.
- `:qa`: Quit all open files/buffers.
- `:wqa`: Save and quit all open files/buffers.

### Navigation

#### Basic Movement
- `h`: Move left.
- `j`: Move down.
- `k`: Move up.
- `l`: Move right.

#### Word Movement
- `w`: Move to the start of the next word.
- `b`: Move to the start of the previous word.
- `e`: Move to the end of the current/next word.

#### Line Movement
- `0`: Move to the start of the line.
- `$`: Move to the end of the line.
- `^`: Move to the first non-blank character.

#### Screen/Document Movement
- `gg`: Go to the first line.
- `G`: Go to the last line.
- `<number>G`: Go to a specific line (e.g., `10G` for line 10).
- `Ctrl-u`: Scroll up half a screen.
- `Ctrl-d`: Scroll down half a screen.
- `Ctrl-f`: Scroll forward one screen.
- `Ctrl-b`: Scroll backward one screen.

#### Jumping
- `%`: Jump to matching parenthesis, bracket, or brace.
- `[[` or `]]`: Jump to previous/next section (useful in code).

### Editing

- `x`: Delete the character under the cursor.
- `dd`: Delete (cut) the current line.
- `<number>dd`: Delete multiple lines (e.g., `3dd` deletes 3 lines).
- `dw`: Delete from cursor to end of the word.
- `d$`: Delete from cursor to end of the line.
- `D`: Same as `d$`.
- `c`: Change (delete and enter insert mode, e.g., `cw` to change a word).
- `r`: Replace the character under the cursor.
- `R`: Enter replace mode (overwrite text).
- `u`: Undo the last change.
- `Ctrl-r`: Redo.
- `.`: Repeat the last change.
- `yy`: Yank (copy) the current line.
- `<number>yy`: Yank multiple lines (e.g., `3yy` copies 3 lines).
- `yw`: Yank a word.
- `p`: Paste after the cursor.
- `P`: Paste before the cursor.

### Search and Replace

- `/<pattern>`: Search forward for a pattern (press `Enter`).
- `?<pattern>`: Search backward for a pattern.
- `n`: Move to the next search match.
- `N`: Move to the previous search match.
- `*`: Search forward for the word under the cursor.
- `#`: Search backward for the word under the cursor.
- `:%s/old/new/g`: Replace all occurrences of "old" with "new".
- `:%s/old/new/gc`: Replace with confirmation.

### Visual Mode Commands

- `v`: Select text character by character.
- `V`: Select entire lines.
- `Ctrl-v`: Select a block (columnar editing).
- **After selecting**:
  - `d`: Delete selected text.
  - `y`: Yank (copy) selected text.
  - `c`: Change selected text.

## 3. Working with Files and Buffers

- `:e <filename>`: Open a new file.
- `:ls`: List open buffers.
- `:b <number>`: Switch to a specific buffer (e.g., `:b2`).
- `:bn`: Go to the next buffer.
- `:bp`: Go to the previous buffer.
- `:bd`: Delete (close) the current buffer.
- `:sp <filename>`: Split window horizontally and open a file.
- `:vsp <filename>`: Split window vertically and open a file.
- `Ctrl-w w`: Switch between split windows.
- `:tabnew <filename>`: Open a file in a new tab.
- `:tabn`: Go to the next tab.
- `:tabp`: Go to the previous tab.

## 4. Advanced Commands for IDE-Like Usage

### Code Navigation

- `gf`: Go to the file under the cursor (e.g., imports).
- `gd`: Go to the definition of the word under the cursor (requires ctags).
- `]d`: Go to the next diagnostic (with a linter plugin).
- `[d`: Go to the previous diagnostic.

### Folding (Code Organization)

- `za`: Toggle a fold.
- `zR`: Open all folds.
- `zM`: Close all folds.

### Command Execution

- `:!<command>`: Run a shell command (e.g., `:!ls`).
- `:make`: Run the make command (for compiling).
- `:sh`: Open a shell within Vim (exit with `exit`).

### Registers and Macros

- `"<letter>y`: Yank to a specific register (e.g., `"ay`).
- `"<letter>p`: Paste from a specific register (e.g., `"ap`).
- `q<letter>`: Start recording a macro (e.g., `qa`).
- `q`: Stop recording.
- `@<letter>`: Replay the macro (e.g., `@a`).
- `@@`: Replay the last macro.

## 5. Customization and Plugins

### Configuration Commands

- `:set <option>`: Set an option (e.g., `:set number`).
- `:set no<option>`: Disable an option (e.g., `:set nonumber`).
- **Common options**:
  - `:set number`: Show line numbers.
  - `:set relativenumber`: Show relative line numbers.
  - `:set autoindent`: Enable auto-indentation.
  - `:set tabstop=4`: Set tab width to 4 spaces.
  - `:set shiftwidth=4`: Set indentation width.
  - `:set expandtab`: Use spaces instead of tabs.
  - `:set ignorecase`: Ignore case in searches.
  - `:set smartcase`: Case-sensitive search if uppercase is used.

### Recommended Plugins

Use a plugin manager like Vim-Plug or Vundle. Install with `:PlugInstall` (for Vim-Plug). Key plugins:

- **NERDTree**: File explorer (`:NERDTreeToggle`).
- **fzf.vim**: Fuzzy file finder (`:Files`, `:Rg` for search).
- **ale**: Asynchronous linting (`:ALENext`, `:ALEPrevious`).
- **vim-surround**: Easy surround editing (e.g., `cs"'` to change `"` to `'`).
- **coc.nvim**: IntelliSense for autocompletion/lsp (`:CocInstall coc-pyright` for Python).
- **ctags or gutentags**: Tag navigation for code (`:tag <symbol>`).
- **vim-fugitive**: Git integration (`:Gstatus`, `:Gcommit`).

### Sample `~/.vimrc`

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

## 6. Miscellaneous Tips

- **Help System**: Use `:h <topic>` (e.g., `:h :w` for save command details).
- **Repeat Commands**: Use `<number><command>` (e.g., `5j` to move down 5 lines).
- **Split Windows**: Combine `:sp` or `:vsp` with `Ctrl-w` commands.
- **Practice**: Run `vimtutor` in the terminal for interactive practice.
- **Cheat Sheet**: Keep a Vim cheat sheet handy.

## 7. Example Workflow

1. Open a file: `vim code.py`.
2. Navigate to line 10: `10G`.
3. Insert text: `i`, type, then `Esc`.
4. Search for a variable: `/my_var<Enter>`, move with `n`.
5. Replace text: `:%s/old/new/g`.
6. Save and quit: `:wq`.
7. Run a command: `:!python code.py`.

## 8. Further Assistance

- **Language-Specific Setup**: Need Python, JavaScript, etc., configurations? Ask for tailored suggestions.
- **Plugin Installation**: Want help with Vim-Plug or specific plugins? I can guide you.
- **Keybindings**: Need custom mappings (e.g., `jj` to `Esc`)? I can provide examples.
- **Neovim**: Using Neovim? Most commands are the same, but I can highlight differences.