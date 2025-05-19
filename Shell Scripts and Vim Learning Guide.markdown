# Step-by-Step Guide to Learning Shell Scripts and Vim

## **1. Introduction to Shell Scripts**
Shell scripts are text files containing Linux commands executed by a shell (typically Bash) to automate tasks. They are powerful for system administration, file manipulation, and process automation.

- **Why Use Shell Scripts?**
  - Automate repetitive tasks (e.g., backups, log analysis).
  - Combine multiple commands into a single script.
  - Support variables, conditionals, loops, and command-line arguments.
  - Portable across Linux systems with Bash.

- **Shell Environment**:
  - Default shell in Linux is often Bash (`/bin/bash`).
  - Check current shell: `echo $SHELL`.
  - Change shell: `chsh -s /bin/bash`.

## **2. Creating and Running Shell Scripts**
Shell scripts are created as text files with a `.sh` extension and executed after making them executable.

- **Steps to Create a Shell Script**:
  1. Create a file: Use Vim or another editor (e.g., `vim myscript.sh`).
  2. Add a shebang line to specify the shell: `#!/bin/bash`.
  3. Write commands, e.g.:
     ```bash
     #!/bin/bash
     echo "Hello, World!"
     ls -l
     ```
  4. Save and exit (Vim instructions below).
  5. Make executable: `chmod +x myscript.sh`.
  6. Run the script:
     - `./myscript.sh` (if in current directory).
     - `bash myscript.sh` (runs without executable permission).
     - `/full/path/to/myscript.sh` (using absolute path).

- **Example Script**:
  ```bash
  #!/bin/bash
  echo "Current directory: $(pwd)"
  echo "Listing files:"
  ls -l
  ```

- **Running Tips**:
  - Ensure the script is in your PATH for global execution: `export PATH=$PATH:/path/to/scripts`.
  - Debug scripts with `bash -x myscript.sh` to trace execution.

## **3. Shell Script Positional Parameters**
Positional parameters allow scripts to accept command-line arguments, similar to C’s `argc` and `argv`.

- **Accessing Parameters**:
  - `$0`: Script name.
  - `$1`, `$2`, ..., `$9`: First to ninth arguments.
  - `$*`: All arguments as a single string.
  - `$@`: All arguments as separate strings.
  - `$#`: Number of arguments.

- **Example Script with Parameters**:
  ```bash
  #!/bin/bash
  echo "Script name: $0"
  echo "First argument: $1"
  echo "Second argument: $2"
  echo "All arguments: $*"
  echo "Number of arguments: $#"
  ```
  - Run: `./myscript.sh one two three`
  - Output:
    ```
    Script name: ./myscript.sh
    First argument: one
    Second argument: two
    All arguments: one two three
    Number of arguments: 3
    ```

- **Shifting Parameters**:
  - Use `shift N` to skip `N` arguments, making subsequent arguments accessible as `$1`, `$2`, etc.
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

## **4. Shell Script Arrays**
Arrays store multiple values in a single variable, useful for handling lists of data.

- **Creating an Array**:
  ```bash
  arr=(1 2 3 4 5)
  ```
  - Optional declaration: `declare -a arr`.

- **Accessing Array Elements**:
  - All elements: `${arr[*]}` or `${arr[@]}`.
  - Specific element: `${arr[i]}` (e.g., `${arr[0]}` for first element).
  - Number of elements: `${#arr[*]}`.

- **Example Script with Array**:
  ```bash
  #!/bin/bash
  arr=(apple banana orange)
  echo "All fruits: ${arr[*]}"
  echo "First fruit: ${arr[0]}"
  echo "Number of fruits: ${#arr[*]}"
  ```
  - Output:
    ```
    All fruits: apple banana orange
    First fruit: apple
    Number of fruits: 3
    ```

## **5. Shell Configuration Files**
Configuration files like `.bashrc` and `.profile` customize the shell environment.

- **`.bashrc`**:
  - Executed when a new non-login Bash shell starts.
  - Used for aliases, environment variables, and startup commands.
  - Edit: `vim ~/.bashrc`.
  - Example content:
    ```bash
    alias c='clear'
    echo "Welcome to Bash!"
    export PATH=/usr/local/bin:$PATH
    ```
  - Apply changes: Open a new terminal or run `source ~/.bashrc`.

- **`.profile`**:
  - Executed for login shells (e.g., GUI terminals, SSH).
  - Used for environment settings that apply to login sessions.
  - Edit: `vim ~/.profile`.
  - Example: Set default editor to Vim:
    ```bash
    export EDITOR=vim
    ```

## **6. Introduction to Vim**
Vim is a text editor for creating and editing files, including shell scripts. It operates in two modes:
- **Command Mode**: For navigation, copying, cutting, and saving (default mode).
- **Insert Mode**: For typing text.

- **Why Use Vim?**:
  - Lightweight and available on most Linux systems.
  - Highly efficient with keyboard shortcuts.
  - Extensible via configuration (`.vimrc`).

- **Installing Vim**:
  - Install: `sudo apt-get install vim`.
  - Verify: `vim --version`.

## **7. Vim Operations for File Management**
Learn to create, edit, delete, save, and exit files in Vim, essential for lab exams.

- **Starting Vim**:
  - Open a file: `vim filename` (e.g., `vim myscript.sh`).
  - Open multiple files:
    - Horizontally: `vim -o file1 file2`.
    - Vertically: `vim -O file1 file2`.
  - Switch between files: `Ctrl + ww`.

- **Creating a File**:
  - Run `vim myscript.sh` (creates a new file if it doesn’t exist).
  - Enter insert mode: Press `i`.
  - Type content, e.g., `#!/bin/bash`.
  - Save: Press `Esc`, then `:w` and `Enter`.

- **Editing a File**:
  - Open: `vim myscript.sh`.
  - Navigate in command mode:
    - Arrow keys or `h` (left), `j` (down), `k` (up), `l` (right).
    - Jump to line: `:n` (e.g., `:5` for line 5).
  - Enter insert mode: `i` (insert before cursor), `a` (after cursor), `o` (new line below).
  - Edit text, e.g., add `echo "Hello"`.
  - Save: `Esc`, `:w`.

- **Deleting Content**:
  - Delete a line: In command mode, press `dd`.
  - Delete n lines: `:nd` (e.g., `:3d` deletes line 3).
  - Delete range: `:m,nd` (e.g., `:2,4d` deletes lines 2–4).
  - Delete word: `dw` (from cursor to end of word).
  - Delete to end of line: `d$`.

- **Saving a File**:
  - Save: `Esc`, `:w`.
  - Save as new file: `:w newfile.sh`.
  - Save and quit: `:wq` or `ZZ` (uppercase).

- **Exiting Vim**:
  - Quit without saving: `:q!`.
  - Save and quit: `:wq`.
  - Quit if no changes: `:q`.

- **Copying and Pasting**:
  - Copy line: `yy`.
  - Copy n lines: `nyy` (e.g., `3yy`).
  - Copy range: `:m,ny` (e.g., `:2,4y`).
  - Copy word: `yw`.
  - Copy current word: `yiw`.
  - Copy to end of line: `y$`.
  - Copy to start of line: `y^`.
  - Paste: `p` (below cursor), `P` (above cursor).

- **Search and Replace**:
  - Search: `/pattern` (e.g., `/echo`), press `n` for next occurrence.
  - Replace first occurrence in line: `:s/old/new`.
  - Replace all in line: `:s/old/new/g`.
  - Replace all in file: `:%s/old/new/g`.

## **8. Configuring Vim with `.vimrc`**
Customize Vim by editing `~/.vimrc` to set preferences like line numbers and indentation.

- **Creating/Editing `.vimrc`**:
  - Open: `vim ~/.vimrc`.
  - Add settings, e.g.:
    ```vim
    set number          " Show line numbers
    set autoindent      " Auto-indent new lines
    set tabstop=4       " 4 spaces per tab
    set nowrap          " Disable line wrapping
    ```
  - Save: `:wq`.
  - Apply: Restart Vim or run `:source ~/.vimrc`.

- **Example `.vimrc`** (from PDF):
  ```vim
  set number
  set autoindent
  set tabstop=4
  set nowrap
  ```

## **9. Additional Tips for Lab Exam**
- **Shell Script Best Practices**:
  - Always include a shebang (`#!/bin/bash`).
  - Comment code with `#` for clarity.
  - Test scripts in a safe environment.
  - Use `set -e` to exit on errors.

- **Vim Productivity Tips**:
  - Undo: `u` in command mode.
  - Redo: `Ctrl + r`.
  - Repeat last command: `.`.
  - Save frequently during exams to avoid data loss.
  - Practice navigation and editing shortcuts.

- **Common Exam Tasks**:
  - Write a script to process command-line arguments.
  - Edit a script in Vim to fix errors or add functionality.
  - Use `grep` in scripts to search files (e.g., `grep "pattern" file`).
  - Configure `.bashrc` or `.vimrc` for custom settings.

- **Debugging Scripts**:
  - Add `set -x` for debugging output.
  - Check syntax: `bash -n myscript.sh`.
  - Verify permissions: `ls -l myscript.sh`.

## **10. Example Lab Exam Scenario**
**Task**: Create a shell script `greet.sh` that takes a name as an argument and prints a greeting. Edit it in Vim, save, make executable, and run it.

- **Solution**:
  1. Open Vim: `vim greet.sh`.
  2. Enter insert mode: `i`.
  3. Write script:
     ```bash
     #!/bin/bash
     echo "Hello, $1!"
     ```
  4. Save and exit: `Esc`, `:wq`.
  5. Make executable: `chmod +x greet.sh`.
  6. Run: `./greet.sh Alice`.
     - Output: `Hello, Alice!`
  7. Edit to add error handling:
     - Open: `vim greet.sh`.
     - Modify:
       ```bash
       #!/bin/bash
       if [ $# -eq 0 ]; then
           echo "Error: Please provide a name."
           exit 1
       fi
       echo "Hello, $1!"
       ```
     - Save: `:wq`.
     - Test: `./greet.sh` (shows error), `./greet.sh Bob` (shows `Hello, Bob!`).

## **11. Additional Resources**
- **Shell Scripting**:
  - [Bash Guide for Beginners](https://tldp.org/LDP/Bash-Beginners-Guide/html/)
  - [Advanced Bash-Scripting Guide](https://tldp.org/LDP/abs/html/)
- **Vim**:
  - [Vim Documentation](http://vimdoc.sourceforge.net/htmldoc/)
  - [Vim Tutorial](https://www.openvim.com/)
  - Run `vimtutor` for an interactive tutorial.
- **General**:
  - [Linux Documentation Project](https://tldp.org/)
  - [Ubuntu Documentation](https://help.ubuntu.com/)