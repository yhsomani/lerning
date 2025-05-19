# Complete Shell Scripting Tutorial

This tutorial provides a step-by-step guide to learning shell scripting using Bash, from basic concepts to advanced topics, with a detailed focus on regular expressions (regex) at the end. It’s designed for beginners and intermediate users who want to automate tasks, manage systems, or build custom tools.

---

## Introduction to Shell Scripting

### What is a Shell?
A shell is a command-line interface that lets you interact with the operating system by typing commands. It acts as a bridge between you and the system’s kernel, executing commands and managing processes. The most popular shell is **Bash** (Bourne Again SHell), which we’ll use in this tutorial.

### What is a Shell Script?
A shell script is a text file containing a series of shell commands that the shell executes in sequence. Scripts can include variables, loops, conditionals, and functions, making them powerful tools for automation.

### Why Use Shell Scripts?
- **Automation**: Save time by automating repetitive tasks like file backups.
- **Efficiency**: Combine multiple commands into one script.
- **Customization**: Build tools tailored to your needs.

---

## Basic Concepts

### Shebang
Every shell script starts with a **shebang** (`#!`), which tells the system which interpreter to use. For Bash scripts, use:
```bash
#!/bin/bash
```
Save this in a file (e.g., `script.sh`), make it executable with `chmod +x script.sh`, and run it with `./script.sh`.

### Comments
Comments start with `#` and are ignored by the shell. Use them to explain your code:
```bash
# This is a comment
echo "Hello"
```

### Variables
Variables store data. Define them without spaces around the `=` sign:
```bash
name="Alice"
age=25
```
Access them with `$`:
```bash
echo "Name: $name, Age: $age"  # Outputs: Name: Alice, Age: 25
```

### Input and Output
- **Output**: Use `echo` to display text:
  ```bash
  echo "Hello, World!"
  ```
- **Input**: Use `read` to get user input:
  ```bash
  read -p "Enter your name: " username
  echo "Hi, $username!"
  ```

---

## Control Structures

### Conditional Statements
Conditionals let your script make decisions.

- **if statement**:
  ```bash
  if [ "$age" -gt 18 ]; then
      echo "You are an adult."
  fi
  ```
  Here, `-gt` means "greater than."

- **if-else**:
  ```bash
  if [ "$age" -lt 18 ]; then
      echo "You are a minor."
  else
      echo "You are an adult."
  fi
  ```

- **elif** (else if):
  ```bash
  if [ "$age" -lt 13 ]; then
      echo "Child"
  elif [ "$age" -lt 20 ]; then
      echo "Teen"
  else
      echo "Adult"
  fi
  ```

Common test operators:
- `-eq`: Equal
- `-ne`: Not equal
- `-lt`: Less than
- `-gt`: Greater than
- `-le`: Less than or equal
- `-ge`: Greater than or equal

### Loops
Loops repeat commands.

- **for loop**: Iterates over a list:
  ```bash
  for fruit in apple banana cherry; do
      echo "Fruit: $fruit"
  done
  ```

- **while loop**: Runs while a condition is true:
  ```bash
  count=0
  while [ $count -lt 3 ]; do
      echo "Count: $count"
      count=$((count + 1))
  done
  ```

- **until loop**: Runs until a condition is true:
  ```bash
  count=0
  until [ $count -ge 3 ]; do
      echoATP "Count: $count"
      count=$((count + 1))
  done
  ```

### Case Statements
Case statements handle multiple options:
```bash
read -p "Enter a day (mon, tue, etc.): " day
case $day in
    "mon")
        echo "Monday: Start of the week!"
        ;;
    "fri")
        echo "Friday: Almost weekend!"
        ;;
    *)
        echo "Some other day."
        ;;
esac
```

---

## Functions

Functions make code reusable.

### Defining Functions
Define a function with:
```bash
say_hello() {
    echo "Hello, World!"
}
say_hello  # Call the function
```

### Passing Arguments
Use `$1`, `$2`, etc., to access arguments:
```bash
greet() {
    echo "Hello, $1!"
}
greet "Bob"  # Outputs: Hello, Bob!
```

### Returning Values
Return numbers with `return` or strings with `echo`:
```bash
add() {
    echo $(( $1 + $2 ))
}
result=$(add 3 4)
echo "Sum: $result"  # Outputs: Sum: 7
```

---

## Advanced Topics

### Arrays
Arrays store multiple values:
```bash
colors=("red" "blue" "green")
echo ${colors[1]}  # Outputs: blue
echo ${colors[@]}  # Outputs all: red blue green
```

### String Manipulation
- **Length**: `${#string}`
  ```bash
  text="hello"
  echo ${#text}  # Outputs: 5
  ```
- **Substring**: `${string:position:length}`
  ```bash
  echo ${text:1:3}  # Outputs: ell
  ```
- **Replace**: `${string/pattern/replacement}`
  ```bash
  echo ${text/hello/hi}  # Outputs: hi
  ```

### File Handling
- **Read a file**:
  ```bash
  while read line; do
      echo "Line: $line"
  done < "file.txt"
  ```
- **Write to a file**:
  ```bash
  echo "Hello" > file.txt   # Overwrites
  echo "World" >> file.txt  # Appends
  ```

### Error Handling
Use `trap` to catch errors:
```bash
trap 'echo "Error occurred!"; exit 1' ERR
ls nonexistent_file  # Triggers trap
```

---

## Regular Expressions (Regex)

Regex is a powerful way to match and manipulate text patterns in shell scripts, often used with tools like `grep`, `sed`, and `awk`.

### Basics of Regex
- **Literals**: Exact matches (e.g., `cat` matches "cat").
- **Metacharacters**:
  - `.`: Any single character.
  - `*`: Zero or more of the previous character.
  - `+`: One or more (used with `grep -E`).
  - `^`: Start of line.
  - `$`: End of line.
  - `[abc]`: Any character in the set (a, b, or c).
  - `[^abc]`: Any character not in the set.
  - `\`: Escapes special characters.

### Using Regex in Shell Scripts
- **grep**: Search for patterns:
  ```bash
  grep "error" log.txt  # Finds lines with "error"
  grep -E "[0-9]+" data.txt  # Finds numbers
  ```
- **sed**: Replace text:
  ```bash
  sed 's/old/new/g' file.txt  # Replaces "old" with "new"
  ```
- **awk**: Process patterned text:
  ```bash
  awk '/error/ {print $2}' log.txt  # Prints second column of lines with "error"
  ```

### Common Regex Patterns
- **Digits**: `[0-9]` (e.g., matches "5" in "abc5def").
- **Letters**: `[a-zA-Z]` (e.g., matches "a" in "123a456").
- **Word characters**: `\w` (letters, digits, underscore; use with `grep -E`).
- **Whitespace**: `\s` (use with `grep -E`).
- **Email**: `[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}`.

### Practical Examples
1. **Match lines starting with "Log"**:
   ```bash
   grep "^Log" file.txt
   ```
2. **Extract IP addresses**:
   ```bash
   grep -E "[0-9]+\.[0-9]+\.[0-9]+\.[0-9]+" network.log
   ```
3. **Replace digits with "X"**:
   ```bash
   sed 's/[0-9]/X/g' text.txt
   ```
4. **Find words with 3+ letters**:
   ```bash
   grep -E "\b[a-zA-Z]{3,}\b" file.txt
   ```

---

## Practice Tips
- Write small scripts and test them.
- Use `man bash` for detailed documentation.
- Experiment with regex using `grep` and sample text files.

This tutorial equips you with the skills to write shell scripts and harness regex for text processing. Happy scripting!