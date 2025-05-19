# Step-by-Step Guide to Learning Shell Scripts and Vim

## 1. Introduction to Shell Scripts
Shell scripts are text files containing Linux commands executed by a shell, typically Bash, to automate tasks like file manipulation, system administration, or backups. They’re versatile, supporting variables, loops, conditionals, and command-line arguments.

- **Benefits**:
  - Automate repetitive tasks, saving time.
  - Combine multiple commands for complex workflows.
  - Portable across Linux systems with Bash.
  - Easy to debug and modify.

- **Shell Environment**:
  - Bash is the default shell in most Linux distributions (`/bin/bash`).
  - Verify your shell: `echo $SHELL`.
  - Switch to Bash if needed: `chsh -s /bin/bash`.

## 2. Creating and Running Shell Scripts
Shell scripts are created as `.sh` files and made executable to run as programs.

- **Steps to Create a Script**:
  1. Open Vim: `vim myscript.sh`.
  2. Add a shebang line: `#!/bin/bash`.
  3. Write commands, e.g.:
     ```bash
     #!/bin/bash
     echo "Hello, World!"
     ls -l
     ```
  4. Save and exit Vim (see Vim section).
  5. Make executable: `chmod +x myscript.sh`.
  6. Run:
     - `./myscript.sh` (current directory).
     - `bash myscript.sh` (no executable permission needed).
     - `/full/path/to/myscript.sh` (absolute path).

- **Example Script**:
  ```bash
  #!/bin/bash
  echo "Current directory: $(pwd)"
  echo "Listing files:"
  ls -l
  ```

- **Execution Tips**:
  - Add the script’s directory to PATH: `export PATH=$PATH:/path/to/scripts`.
  - Debug with `bash -x myscript.sh` to trace execution.
  - Check permissions: `ls -l myscript.sh`.

| **Command** | **Description** | **Example** |
|-------------|-----------------|-------------|
| `chmod +x <script>` | Makes script executable | `chmod +x myscript.sh` |
| `./<script>` | Runs executable script | `./myscript.sh` |
| `bash <script>` | Runs script without executable permission | `bash myscript.sh` |
| `bash -x <script>` | Debugs script with trace | `bash -x myscript.sh` |

## 3. Positional Parameters in Shell Scripts
Positional parameters allow scripts to process command-line arguments, similar to function arguments in other languages.

- **Key Parameters**:
  - `$0`: Script name.
  - `$1`, `$2`, ..., `$9`: First to ninth arguments.
  - `$*`: All arguments as a single string.
  - `$@`: All arguments as separate strings.
  - `$#`: Number of arguments.

- **Example Script**:
  ```bash
  #!/bin/bash
  echo "Script: $0"
  echo "First arg: $1"
  echo "Second arg: $2"
  echo "All args: $*"
  echo "Arg count: $#"
  ```
  - Run: `./myscript.sh apple banana`
  - Output:
    ```
    Script: ./myscript.sh
    First arg: apple
    Second arg: banana
    All args: apple banana
    Arg count: 2
    ```

- **Shifting Parameters**:
  - `shift N` moves arguments left by `N` positions, making later arguments accessible as `$1`, `$2`, etc.
  - Example:
    ```bash
    #!/bin/bash
    echo "Before shift: $1 $2 $3"
    shift 2
    echo "After shift: $1"
    ```
    - Run: `./myscript.sh a b c`
    - Output:
      ```
      Before shift: a b c
      After shift: c
      ```

| **Parameter** | **Description** | **Example Output** |
|---------------|-----------------|--------------------|
| `$0` | Script name | `./myscript.sh` |
| `$1` | First argument | `apple` |
| `$*` | All arguments | `apple banana` |
| `$#` | Argument count | `2` |

## 4. Arrays in Shell Scripts
Arrays store multiple values in a single variable, useful for lists or iterative tasks.

- **Creating an Array**:
  ```bash
  arr=(red green blue)
  ```
  - Optional: `declare -a arr`.

- **Accessing Elements**:
  - All elements: `${arr[*]}` or `${arr[@]}`.
  - Specific element: `${arr[i]}` (e.g., `${arr[0]}`).
  - Element count: `${#arr[*]}`.

- **Example Script**:
  ```bash
  #!/bin/bash
  arr=(red green blue)
  echo "Colors: ${arr[*]}"
  echo "First color: ${arr[0]}"
  echo "Color count: ${#arr[*]}"
  ```
  - Output:
    ```
    Colors: red green blue
    First color: red
    Color count: 3
    ```

- **Looping Through Arrays**:
  ```bash
  for color in "${arr[@]}"; do
      echo "Color: $color"
  done
  ```

## 5. Shell Configuration Files
Configuration files customize the Bash environment, affecting aliases, variables, and startup behavior.

- **`.bashrc`**:
  - Runs for non-login shells (e.g., new terminal windows).
  - Used for aliases, functions, and environment variables.
  - Edit: `vim ~/.bashrc`.
  - Example:
    ```bash
    alias ll='ls -l'
    export PATH=$PATH:/usr/local/bin
    echo "Bash loaded!"
    ```
  - Apply: `source ~/.bashrc` or open a new terminal.

- **`.profile`**:
  - Runs for login shells (e.g., SSH, GUI login).
  - Sets environment variables for login sessions.
  - Edit: `vim ~/.profile`.
  - Example:
    ```bash
    export EDITOR=vim
    export LANG=en_US.UTF-8
    ```

| **File** | **Purpose** | **When Executed** |
|----------|-------------|-------------------|
| `.bashrc` | Customizes non-login shells | New terminal |
| `.profile` | Sets login shell environment | Login session |

## 6. Introduction to Vim
Vim is a lightweight, keyboard-driven text editor ideal for editing shell scripts. It operates in:
- **Command Mode**: For navigation, copying, deleting, and saving.
- **Insert Mode**: For typing text.

- **Advantages**:
  - Available on most Linux systems.
  - Fast with keyboard shortcuts.
  - Customizable via `.vimrc`.

- **Installation**:
  - Install: `sudo apt-get install vim` ([Ubuntu Documentation](https://help.ubuntu.com/community/Vim)).
  - Verify: `vim --version`.

## 7. Vim File Operations
Master these Vim commands to create, edit, delete, save, and exit files for your exam.

- **Starting Vim**:
  - Open a file: `vim myscript.sh`.
  - Open multiple files:
    - Horizontal split: `vim -o file1 file2`.
    - Vertical split: `vim -O file1 file2`.
  - Switch files: `Ctrl + ww`.

- **Creating a File**:
  - Run: `vim myscript.sh` (creates if non-existent).
  - Enter insert mode: `i`.
  - Type: `#!/bin/bash`.
  - Save: `Esc`, `:w`, `Enter`.

- **Editing a File**:
  - Open: `vim myscript.sh`.
  - Navigate (command mode):
    - `h` (left), `j` (down), `k` (up), `l` (right).
    - Jump to line: `:n` (e.g., `:10`).
  - Insert mode: `i` (before cursor), `a` (after cursor), `o` (new line below).
  - Edit, e.g., add `echo "Test"`.
  - Save: `Esc`, `:w`.

- **Deleting Content**:
  - Line: `dd`.
  - N lines: `:nd` (e.g., `:3d`).
  - Range: `:m,nd` (e.g., `:2,5d`).
  - Word: `dw`.
  - To end of line: `d$`.

- **Saving a File**:
  - Save: `:w`.
  - Save as: `:w newfile.sh`.
  - Save and quit: `:wq` or `ZZ`.

- **Exiting Vim**:
  - Quit without saving: `:q!`.
  - Save and quit: `:wq`.
  - Quit if unchanged: `:q`.

- **Copying and Pasting**:
  - Copy line: `yy`.
  - Copy n lines: `nyy` (e.g., `3yy`).
  - Copy word: `yw`.
  - Paste: `p` (below), `P` (above).

- **Search and Replace**:
  - Search: `/pattern` (e.g., `/echo`), `n` for next.
  - Replace in line: `:s/old/new`.
  - Replace all in file: `:%s/old/new/g`.

| **Vim Command** | **Action** | **Example** |
|-----------------|------------|-------------|
| `:w` | Save file | `:w` |
| `:q!` | Quit without saving | `:q!` |
| `dd` | Delete line | `dd` |
| `yy` | Copy line | `yy` |
| `/pattern` | Search for pattern | `/echo` |

## 8. Configuring Vim with `.vimrc`
Customize Vim’s behavior by editing `~/.vimrc`.

- **Steps**:
  - Open: `vim ~/.vimrc`.
  - Add settings:
    ```vim
    set number
    set autoindent
    set tabstop=4
    set nowrap
    ```
  - Save: `:wq`.
  - Apply: `:source ~/.vimrc` or restart Vim.

- **Common Settings**:
  - `set number`: Show line numbers.
  - `set autoindent`: Auto-indent new lines.
  - `set tabstop=4`: 4 spaces per tab.
  - `syntax on`: Enable syntax highlighting.

## 9. Advanced Shell Scripting Concepts
These topics may appear in your exam for more complex tasks.

- **Conditionals**:
  ```bash
  if [ "$1" == "test" ]; then
      echo "Argument is test"
  else
      echo "Argument is not test"
  fi
  ```

- **Loops**:
  ```bash
  for i in {1..3}; do
      echo "Loop $i"
  done
  ```

- **Functions**:
  ```bash
  greet() {
      echo "Hello, $1!"
  }
  greet "Alice"
  ```

## 10. Lab Exam Preparation Tips
- **Scripting**:
  - Practice scripts with arguments and error handling.
  - Use comments (`#`) for clarity.
  - Test scripts in a sandbox environment.
  - Add `set -e` to exit on errors.

- **Vim**:
  - Memorize shortcuts: `u` (undo), `Ctrl + r` (redo), `.` (repeat).
  - Save often (`:w`) to avoid losing work.
  - Practice split windows and navigation.

- **Debugging**:
  - Script syntax check: `bash -n myscript.sh`.
  - Trace execution: `set -x` inside script.
  - Verify permissions: `ls -l`.

- **Common Tasks**:
  - Write a script to process files (e.g., `grep "error" log.txt`).
  - Edit scripts in Vim to add features or fix bugs.
  - Configure `.bashrc` or `.vimrc`.

## 11. Example Exam Scenario
**Task**: Create a script `backup.sh` that takes a directory as an argument and lists its files. Edit in Vim, add error handling, save, run, and test.

- **Solution**:
  1. Open Vim: `vim backup.sh`.
  2. Insert mode: `i`.
  3. Write:
     ```bash
     #!/bin/bash
     echo "Files in $1:"
     ls -l "$1"
     ```
  4. Save and exit: `Esc`, `:wq`.
  5. Make executable: `chmod +x backup.sh`.
  6. Run: `./backup.sh /tmp`.
  7. Edit for error handling:
     - Open: `vim backup.sh`.
     - Modify:
       ```bash
       #!/bin/bash
       if [ $# -eq 0 ]; then
           echo "Error: Provide a directory."
           exit 1
       fi
       if [ ! -d "$1" ]; then
           echo "Error: $1 is not a directory."
           exit 1
       fi
       echo "Files in $1:"
       ls -l "$1"
       ```
     - Save: `:wq`.
     - Test: `./backup.sh` (error), `./backup.sh /tmp` (lists files).

## 12. Additional Resources
- Practice with `vimtutor` for interactive Vim learning.
- Explore Bash scripting tutorials for advanced topics.
- Use Linux man pages: `man bash`, `man vim`.