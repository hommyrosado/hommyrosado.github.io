---
title: Bash
layout: default
nav_order: 2
---

# Bash
{: .no_toc }

---
jupyter:
  kernelspec:
    display_name: Python 3
    language: python
    name: python3
  language_info:
    codemirror_mode:
      name: ipython
      version: 3
    file_extension: .py
    mimetype: text/x-python
    name: python
    nbconvert_exporter: python
    pygments_lexer: ipython3
    version: 3.12.5
  nbformat: 4
  nbformat_minor: 2
---

::: {.cell .markdown}
Exclamation Mark: In Jupyter Notebook, both ! and % can be used to
execute shell commands, but they serve different purposes and have
different scopes. ! (Exclamation Mark)

-   The ! character is used to execute shell commands directly from
    within a Jupyter Notebook cell.

-   When you use !, you are essentially calling the command line
    interface (CLI) of your system. For example:
:::

::: {.cell .code execution_count="44"}
``` python
%ls -la
#files = %ls -la
#files
!echo hello, this world
!echo "hello from withing quotes"
```

::: {.output .stream .stdout}
     Volume in drive C is OS
     Volume Serial Number is 30F1-DDB5

     Directory of c:\Repos\Bash_Study
:::

::: {.output .stream .stderr}
    File Not Found
:::

::: {.output .stream .stdout}
    hello, this world
    "hello from withing quotes"
:::
:::

::: {.cell .markdown}
Magic commands: Using the % \... %timeit x = sum(range(1000)) Some
common magic commands include:

-   %timeit: Time execution of a Python statement.
-   %run: Run a Python script.
-   %env: Set environment variables.
-   %pwd: Print the current working directory.
-   %%bash: Run a cell of bash commands.
:::

::: {.cell .code execution_count="54"}
``` python
%pwd
#%timeit x = sum(range(1000))
```

::: {.output .execute_result execution_count="54"}
    'c:\\Repos\\Bash_Study'
:::
:::

::: {.cell .markdown}
Use ! when you want to run a shell command directly as if you were in a
terminal. Use % for magic commands that perform specific actions within
the notebook environment, often related to Python or the notebook
itself.
:::

::: {.cell .markdown}
The type \[type COMMAND\] built-in shell command in Bash is used to
display information about a command\'s type. It tells you how the shell
interprets a command, whether it is a built-in command, an alias, a
function, or an external command (an executable file).
Example: type \[options\] name
Common Options

-   -t: Print a single word which is one of \"alias\", \"keyword\",
    \"function\", \"builtin\", \"file\", or \"name\" if name is not
    found.
-   -a: Display all of the places that contain an executable named name.
    This includes aliases, built-ins, and functions, as well as files in
    the \$PATH.
-   -p: Displays the path to the executable that would have been
    executed, if name is an external command.
:::

::: {.cell .markdown}
\$ type -a test test is a shell builtin test is /usr/bin/test test is
/bin/test test is /usr/bin/test

Example to find all locations of a command: `<br>`{=html} type -a echo
echo is a shell builtin
echo is /usr/bin/echo
echo is /bin/echo
echo is /usr/bin/echo

`<br>`{=html}type \--help type: type \[-afptP\] name \[name \...\]
`<br>`{=html}Display information about command type.

    For each NAME, indicate how it would be interpreted if used as a
    command name.

    Options:
      -a        display all locations containing an executable named NAME;
                includes aliases, builtins, and functions, if and only if
                the `-p' option is not also used
      -f        suppress shell function lookup
      -P        force a PATH search for each NAME, even if it is an alias,
                builtin, or function, and returns the name of the disk file
                that would be executed
      -p        returns either the name of the disk file that would be executed,
                or nothing if `type -t NAME' would not return `file'
      -t        output a single word which is one of `alias', `keyword',
                `function', `builtin', `file' or `', if NAME is an alias,
                shell reserved word, shell function, shell builtin, disk file,
                or not found, respectively

    Arguments:
      NAME      Command name to be interpreted.

    Exit Status:
    Returns success if all of the NAMEs are found; fails if any are not found.
:::

::: {.cell .markdown}
What is the difference between the .bash_profile, .bashrc, and .profile?
The .bash_profile, .bashrc, and .profile files are all configuration
scripts for shell environments in Unix-like operating systems, but they
serve different purposes and are executed in different scenarios.
Here\'s a breakdown of each:

1.  .bash_profile Purpose: The .bash_profile script is executed
    automatically when a user logs in using a Bash login shell. This is
    typically the shell you see when you log in to a system remotely via
    SSH or start a terminal session in a text mode console. Usage: It\'s
    used to set up environment variables, paths, and other startup
    programs that should be configured once per session. Execution: It
    runs only once at the start of a login session.
2.  .bashrc Purpose: The .bashrc script is executed for non-login
    interactive shells. This typically includes new terminal windows or
    tab sessions in a graphical desktop environment. Usage: It\'s mainly
    used to configure the shell environment, such as setting aliases,
    functions, and shell options that should be available in every
    interactive shell session. Execution: It runs every time a new shell
    session is opened.
3.  .profile Purpose: The .profile script is similar to .bash_profile
    but is more general and can be used by other shells like sh, dash,
    or ksh. Usage: It is often used in environments where multiple types
    of shells are in use or when the system defaults to a different
    shell than Bash. It typically sets up environment variables and can
    call .bash_profile or .bashrc if Bash-specific settings are needed.
    Execution: Like .bash_profile, it runs at the start of a login
    session but is more shell-agnostic. Summary: .bash_profile: Executed
    for login shells, usually at the start of a session, mainly for
    environment settings. .bashrc: Executed for non-login interactive
    shells, mainly for configuring the interactive environment.
    .profile: A more general startup script executed for login shells,
    especially in environments where different shells might be used.
    Typical Setup: On many systems, .bash_profile is configured to
    source (include) .bashrc to ensure that the settings in .bashrc are
    applied even during login sessions:

Example code:

if \[ -f \~/.bashrc \]; then
. \~/.bashrc
fi
:::

::: {.cell .markdown}
Means by which to execute your .sh files: To run a `.sh` (shell script)
file, you can follow these steps:

### 1. **Make the Script Executable (if it's not already)** {#1-make-the-script-executable-if-its-not-already}

Before running a shell script, ensure it has execute permissions. You
can do this using the `chmod` command:

``` bash
chmod +x script_name.sh
```

This command makes the script executable.

### 2. **Execute the Script** {#2-execute-the-script}

There are a few different ways to run the script:

#### a) **Run the Script with `./`** {#a-run-the-script-with-}

This is the most common method. Navigate to the directory where the
script is located and run it using `./`:

``` bash
./script_name.sh
```

#### b) **Run the Script with `bash` or `sh`**

If you don't want to change permissions, you can explicitly run the
script using `bash` or `sh`:

``` bash
bash script_name.sh
```

or

``` bash
sh script_name.sh
```

### Example:

Let's say you have a script called `hello_world.sh`:

``` bash
#!/bin/bash
echo "Hello, World!"
```

1.  **Make it executable**:

    ``` bash
    chmod +x hello_world.sh
    ```

2.  **Run the script**:

    ``` bash
    ./hello_world.sh
    ```

    or

    ``` bash
    bash hello_world.sh
    ```

This will output:

    Hello, World!

### Note:

-   If the script is in a directory that's included in your `PATH`
    environment variable, you can run it just by typing
    `script_name.sh`.
-   Always ensure the first line of your script (`#!/bin/bash`)
    correctly points to the interpreter you want to use (in this case,
    Bash).
:::

::: {.cell .markdown}
In Bash, both `echo` and `printf` are used to display text or output
data to the terminal. However, they have some key differences in
functionality, behavior, and usage. Here's a comparison:

### 1. **Basic Syntax** {#1-basic-syntax}

-   **`echo`**:

    ``` bash
    echo "Hello, World!"
    ```

-   **`printf`**:

    ``` bash
    printf "%s\n" "Hello, World!"
    ```

### 2. **Usage** {#2-usage}

-   **`echo`**:
    -   `echo` is simpler and easier to use for basic output.

    -   It automatically adds a newline character at the end of the
        output unless suppressed with the `-n` option.

    -   It has less formatting control compared to `printf`.

    -   Example:

        ``` bash
        echo "Hello, World!"
        ```
-   **`printf`**:
    -   `printf` is more powerful and flexible, similar to the C
        language's `printf` function.

    -   It does not add a newline character automatically; you need to
        include it explicitly using `\n`.

    -   It provides more control over formatting, making it suitable for
        more complex output needs, such as formatting numbers, aligning
        text, etc.

    -   Example:

        ``` bash
        printf "%s\n" "Hello, World!"
        ```

### 3. **Portability** {#3-portability}

-   **`echo`**:
    -   `echo` may behave differently across different systems or shells
        (e.g., with how it handles special characters like `-e` or
        backslashes).
    -   Some implementations of `echo` treat options like `-e` (to
        enable interpretation of backslash escapes) and `-n` (to
        suppress newline) differently.
-   **`printf`**:
    -   `printf` is more consistent across different environments
        because it adheres more closely to POSIX standards.
    -   It\'s more reliable for scripts that need to be portable across
        different Unix-like systems.

### 4. **Special Characters and Escape Sequences** {#4-special-characters-and-escape-sequences}

-   **`echo`**:
    -   Handles escape sequences depending on the options used (e.g.,
        `-e` for enabling backslash escapes).

    -   Example with escape sequence:

        ``` bash
        echo -e "Line1\nLine2"
        ```
-   **`printf`**:
    -   Provides precise control over escape sequences and formatting.

    -   Example with escape sequence:

        ``` bash
        printf "Line1\nLine2\n"
        ```

### 5. **Formatting Capabilities** {#5-formatting-capabilities}

-   **`echo`**:
    -   Limited formatting capabilities. Mostly used for simple text
        output.
-   **`printf`**:
    -   Offers advanced formatting, similar to C\'s `printf`. You can
        format strings, numbers, align text, and more.

    -   Example of formatting a number:

        ``` bash
        printf "Number: %04d\n" 5
        ```

        Output: `Number: 0005`

### Summary:

-   **Use `echo`**: When you need simple, quick text output with minimal
    formatting needs.
-   **Use `printf`**: When you need precise control over formatting,
    need to print data without an automatic newline, or require more
    advanced output formatting.

In scripts, it\'s generally a good idea to use `printf` for consistency
and portability, especially when complex formatting is involved.
:::

::: {.cell .markdown}
In Bash scripting, positional parameters, special parameters, and
variables play a crucial role in controlling the behavior of scripts and
passing data. Here's an overview of each:

### 1. **Positional Parameters** {#1-positional-parameters}

Positional parameters are used to pass arguments to a Bash script or
function. They are accessed using numbers (`$1`, `$2`, etc.)
corresponding to their position on the command line or within a function
call.

-   **\$0**: The name of the script or function being executed.
-   **\$1, \$2, \..., \$N**: The first, second, \..., nth arguments
    passed to the script or function.
-   **\$#**: The number of positional parameters (i.e., the number of
    arguments).
-   **\$@**: All positional parameters as separate words.
-   **\$**\*: All positional parameters as a single word.

**Example**:

``` bash
#!/bin/bash
echo "Script name: $0"
echo "First argument: $1"
echo "Second argument: $2"
echo "Number of arguments: $#"
echo "All arguments (individually): $@"
echo "All arguments (as a single string): $*"
```

**Usage**:

``` bash
./myscript.sh arg1 arg2
```

**Output**:

    Script name: ./myscript.sh
    First argument: arg1
    Second argument: arg2
    Number of arguments: 2
    All arguments (individually): arg1 arg2
    All arguments (as a single string): arg1 arg2

### 2. **Special Parameters** {#2-special-parameters}

Special parameters are predefined variables in Bash that provide
information about the script\'s execution environment and status.

-   **\$?**: The exit status of the last command executed (0 for
    success, non-zero for failure).
-   **\$\$**: The process ID (PID) of the current shell.
-   **\$!**: The PID of the last background command.
-   **\$-**: The current options set for the shell (e.g., `-x` for
    debugging).
-   \*\*\$\_\*\*: The last argument of the previous command or the last
    word of the previous command executed.

**Example**:

``` bash
#!/bin/bash
echo "PID of the script: $$"
echo "Last background command PID: $!"
echo "Exit status of the last command: $?"
echo "Last argument of the previous command: $_"
```

### 3. **Variables** {#3-variables}

Variables in Bash are used to store and manipulate data. You can create
your own variables or use environment variables that are predefined by
the system.

-   **User-defined Variables**:
    -   You can define variables by assigning them a value. No spaces
        should surround the `=` sign.

    -   Example:

        ``` bash
        name="Alice"
        echo "Hello, $name!"
        ```
-   **Environment Variables**:
    -   These are predefined variables that affect the behavior of the
        shell and user environment.
    -   Common examples include:
        -   **`$HOME`**: The current user's home directory.
        -   **`$PATH`**: A colon-separated list of directories that the
            shell searches for commands.
        -   **`$USER`**: The current user's username.
        -   **`$SHELL`**: The path to the current shell.
        -   **`$PWD`**: The current working directory.
-   **Variable Scope**:
    -   **Local Variables**: Defined within a script or function and not
        accessible outside of that scope.
    -   **Global Variables**: Defined and available in the current shell
        session and any scripts or commands called from it.

**Example of User-defined and Environment Variables**:

``` bash
#!/bin/bash
name="Alice"
echo "Hello, $name!"
echo "Your home directory is $HOME"
echo "Your current shell is $SHELL"
```

### Summary {#summary}

-   **Positional Parameters**: Used to access arguments passed to a
    script or function, like `$1`, `$2`, `$@`, etc.
-   **Special Parameters**: Predefined variables like `$?`, `$$`, `$!`,
    etc., that provide information about the script and its execution
    environment.
-   **Variables**: Store data for use within the script, with
    user-defined variables and environment variables being the two main
    types.
:::

::: {.cell .markdown}
In Bash scripting, arguments (or parameters) allow you to pass data to a
script or function. Here\'s a comprehensive overview of how arguments
work in Bash:

### 1. **Passing Arguments to a Script** {#1-passing-arguments-to-a-script}

When you run a Bash script, you can pass arguments to it directly from
the command line. These arguments are accessed within the script using
positional parameters.

**Example Script (`example.sh`):**

``` bash
#!/bin/bash

echo "Script name: $0"
echo "First argument: $1"
echo "Second argument: $2"
echo "All arguments as a single string: $*"
echo "All arguments as separate words: $@"
echo "Number of arguments: $#"
```

**Running the Script:**

``` bash
./example.sh arg1 arg2 arg3
```

**Output:**

    Script name: ./example.sh
    First argument: arg1
    Second argument: arg2
    All arguments as a single string: arg1 arg2 arg3
    All arguments as separate words: arg1 arg2 arg3
    Number of arguments: 3

### Explanation of Positional Parameters:

-   **`$0`**: The name of the script.
-   **`$1, $2, ..., $N`**: The first, second, \..., nth arguments passed
    to the script.
-   **`$#`**: The number of arguments passed to the script.
-   **`$@`**: All the arguments passed to the script, treated as
    separate words.
-   **`$*`**: All the arguments passed to the script, treated as a
    single word.

### 2. **Handling Arguments in Functions** {#2-handling-arguments-in-functions}

You can also pass arguments to functions within a Bash script.

**Example Script:**

``` bash
#!/bin/bash

greet() {
    echo "Hello, $1!"
    echo "You passed $# arguments."
}

greet "Alice"
greet "Bob" "and Carol"
```

**Output:**

    Hello, Alice!
    You passed 1 arguments.
    Hello, Bob!
    You passed 2 arguments.

### 3. **Special Parameters** {#3-special-parameters}

-   **`$?`**: The exit status of the last command executed (0 for
    success, non-zero for failure).
-   **`$$`**: The process ID of the current shell.
-   **`$!`**: The process ID of the last background command.
-   **`$_`**: The last argument of the previous command.

### 4. **Using `shift` to Handle Arguments** {#4-using-shift-to-handle-arguments}

The `shift` command is used to shift the positional parameters to the
left. This effectively discards the first argument and moves all other
arguments one position down.

**Example Script:**

``` bash
#!/bin/bash

while [ $# -gt 0 ]; do
    echo "Processing argument: $1"
    shift
done
```

**Running the Script:**

``` bash
./example.sh arg1 arg2 arg3
```

**Output:**

    Processing argument: arg1
    Processing argument: arg2
    Processing argument: arg3

### 5. **Quoting Arguments** {#5-quoting-arguments}

When passing arguments that contain spaces or special characters, it\'s
essential to quote them to ensure they\'re treated as single arguments.

**Example Script:**

``` bash
#!/bin/bash

echo "First argument: $1"
```

**Running the Script:**

``` bash
./example.sh "Hello, World!"
```

**Output:**

    First argument: Hello, World!

### 6. **Default Values for Arguments** {#6-default-values-for-arguments}

You can assign default values to arguments if they are not provided.

**Example Script:**

``` bash
#!/bin/bash

name=${1:-"Default Name"}
echo "Hello, $name!"
```

**Running the Script:**

``` bash
./example.sh
```

**Output:**

    Hello, Default Name!

### Summary {#summary}

-   **Positional Parameters**: Accessed using `$1`, `$2`, etc., they
    allow you to retrieve arguments passed to the script.
-   **Special Parameters**: Provide information about the script\'s
    execution (`$?`, `$$`, `$!`, etc.).
-   **Functions**: Arguments can also be passed to functions, and
    handled similarly to how they are in the script.
-   **`shift`**: Useful for processing arguments in a loop by discarding
    the first argument each time.
-   **Quoting**: Important for handling arguments with spaces or special
    characters.
-   **Default Values**: Can be set using parameter expansion to ensure
    your script behaves predictably when arguments are missing.
:::

::: {.cell .code execution_count="77"}
``` python
#Practice with arguments
!echo 1 '2 3' 4 5

!echo -n Now\ is the time
# %printf "%s %s\n" one two three

```

::: {.output .stream .stdout}
    1 '2 3' 4 5
    -n Now\ is the time
:::

::: {.output .stream .stderr}
    UsageError: Line magic function `%printf` not found.
:::
:::

::: {.cell .markdown}
The `xpg_echo` option in Bash relates to how the `echo` command behaves
with respect to the interpretation of escape sequences. This option is
tied to the way the `echo` command handles certain flags and whether it
conforms to the POSIX X/Open Portability Guide (XPG) standard.

### Understanding `xpg_echo`

-   **Default Behavior of `echo`**: By default, the behavior of the
    `echo` command in Bash can vary slightly depending on the system and
    the version of Bash you are using. Typically, `echo` does not
    interpret escape sequences (like `\n` for newline or `\t` for tab)
    unless explicitly instructed to do so using the `-e` flag (e.g.,
    `echo -e "Hello\nWorld"`).

-   **`xpg_echo` Enabled**: When the `xpg_echo` option is enabled, the
    `echo` command treats escape sequences according to the XPG
    standard. This means that `echo` will automatically interpret escape
    sequences without needing the `-e` flag.

### How to Use `xpg_echo`

-   **Checking `xpg_echo` Status**: You can check if the `xpg_echo`
    option is currently enabled or disabled using the `shopt` command:

    ``` bash
    shopt xpg_echo
    ```

    -   If `xpg_echo` is enabled, you\'ll see `xpg_echo     on`.
    -   If it\'s disabled, you\'ll see `xpg_echo     off`.

-   **Enabling/Disabling `xpg_echo`**: You can enable or disable the
    `xpg_echo` option using the `shopt` command:

    -   **Enable `xpg_echo`**:

        ``` bash
        shopt -s xpg_echo
        ```

    -   **Disable `xpg_echo`**:

        ``` bash
        shopt -u xpg_echo
        ```

### Example of `xpg_echo` Behavior

1.  **Without `xpg_echo` (Default Behavior)**:

    ``` bash
    shopt -u xpg_echo
    echo "Hello\nWorld"
    ```

    **Output**:

        Hello\nWorld

    The escape sequence `\n` is treated as a literal string.

2.  **With `xpg_echo` Enabled**:

    ``` bash
    shopt -s xpg_echo
    echo "Hello\nWorld"
    ```

    **Output**:

        Hello
        World

    The escape sequence `\n` is interpreted as a newline, resulting in
    the text being split across two lines.

### Key Points

-   The `xpg_echo` option controls whether the `echo` command
    automatically interprets escape sequences.
-   The behavior of `echo` with `xpg_echo` enabled aligns with the POSIX
    XPG standard, which can be important for writing portable scripts
    across different Unix-like systems.
-   By default, `xpg_echo` is usually disabled, meaning escape sequences
    are not interpreted unless `-e` is used with `echo`.

Enabling or disabling `xpg_echo` should be done with caution, especially
in scripts meant to run on different environments, as it might lead to
unexpected results if the script relies on specific `echo` behaviors.
:::

::: {.cell .markdown}
Here are examples of how each of these escape sequences works in Bash
using the `printf` command:

``` bash
# \a: Alert (Bell) - Produces a beep sound
printf "\a:: Alert (Bell)\n"

# \b: Backspace - Deletes the previous character (if applicable)
printf "Hello\b: Backspace\n"

# \e: Escape character - Often used in terminal control sequences (here it prints the escape character)
printf "\e:: Escape character\n"

# \f: Form feed - Advances the text to the next "page" (not usually visible in terminals, more relevant in printers)
printf "Hello\f: Form feed\n"

# \n: Newline - Moves the cursor to the next line
printf "Hello\n: Newline\n"

# \r: Carriage return - Returns the cursor to the beginning of the line (overwrites the text)
printf "Hello\r: Carriage return\n"

# \t: Horizontal tab - Inserts a horizontal tab space
printf "Hello\t: Horizontal tab\n"

# \v: Vertical tab - Advances the text to the next vertical tab stop (similar to a newline but may cause issues in some terminals)
printf "Hello\v: Vertical tab\n"

# \\: Backslash - Prints a backslash
printf "\\: Backslash\n"

# \nnn: A character specified by one to three octal digits
# Example: \101 is 'A' in octal
printf "\101: Octal 'A'\n"

# \xHH: A character specified by one or two hexadecimal digits
# Example: \x41 is 'A' in hexadecimal
printf "\x41: Hexadecimal 'A'\n"
```

### Explanation of Each Example:

1.  **`\a: Alert (Bell)`**: Produces an audible bell or beep (if your
    terminal supports it). This is useful for getting attention, for
    example, in error notifications.

    ``` bash
    printf "\a:: Alert (Bell)\n"
    ```

2.  **`\b: Backspace`**: Moves the cursor one position to the left,
    effectively deleting the character before it if additional
    characters are printed afterward.

    ``` bash
    printf "Hello\b: Backspace\n"
    ```

    **Output**: The `o` in `Hello` is removed, and the text becomes
    `Hell: Backspace`.

3.  **`\e: Escape character`**: Represents the escape character, often
    used in ANSI escape codes for terminal control.

    ``` bash
    printf "\e:: Escape character\n"
    ```

    **Output**: Prints the escape character (this might not visibly
    produce an output).

4.  **`\f: Form feed`**: Advances the terminal to the next form feed
    position (similar to a page break in printers). Most terminals
    won\'t visibly do much with this.

    ``` bash
    printf "Hello\f: Form feed\n"
    ```

5.  **`\n: Newline`**: Moves the cursor to the beginning of the next
    line.

    ``` bash
    printf "Hello\n: Newline\n"
    ```

6.  **`\r: Carriage return`**: Moves the cursor to the beginning of the
    current line, causing subsequent text to overwrite what was
    previously written.

    ``` bash
    printf "Hello\r: Carriage return\n"
    ```

    **Output**: The text `: Carriage return` overwrites `Hello`.

7.  **`\t: Horizontal tab`**: Inserts a horizontal tab space, which
    generally equates to about 8 spaces in most terminals.

    ``` bash
    printf "Hello\t: Horizontal tab\n"
    ```

8.  **`\v: Vertical tab`**: Moves the text to the next vertical tab
    stop. This may act similarly to a newline, though it's less commonly
    used and can behave differently in various terminals.

    ``` bash
    printf "Hello\v: Vertical tab\n"
    ```

9.  **`\\: Backslash`**: Prints a literal backslash character.

    ``` bash
    printf "\\: Backslash\n"
    ```

10. **`\nnn: A character specified by one to three octal digits`**:
    Prints the character corresponding to the octal value. For example,
    `\101` corresponds to the letter `A`.

    ``` bash
    printf "\101: Octal 'A'\n"
    ```

11. **`\xHH: A character specified by one or two hexadecimal digits`**:
    Prints the character corresponding to the hexadecimal value. For
    example, `\x41` corresponds to the letter `A`.

    ``` bash
    printf "\x41: Hexadecimal 'A'\n"
    ```

### Running These Examples:

To see the results, you can copy and paste these commands into a Bash
terminal. The effects of some escape sequences, like `\a` (Alert) and
`\f` (Form feed), may depend on your terminal\'s capabilities.
:::

::: {.cell .markdown}
In Bash, the `printf` command supports a variety of format specifiers
that allow you to control the formatting of output data. These
specifiers are similar to those in C\'s `printf` function. Here are some
examples of how to use these format specifiers in Bash:

### 1. **String Specifier: `%s`** {#1-string-specifier-s}

The `%s` specifier is used to format strings.

``` bash
printf "Hello, %s!\n" "World"
```

**Output:**

    Hello, World!

### 2. **Decimal Integer Specifier: `%d`** {#2-decimal-integer-specifier-d}

The `%d` specifier is used to format decimal integers.

``` bash
printf "Number: %d\n" 42
```

**Output:**

    Number: 42

### 3. **Floating-Point Specifier: `%f`** {#3-floating-point-specifier-f}

The `%f` specifier is used to format floating-point numbers.

``` bash
printf "Pi is approximately %f\n" 3.14159
```

**Output:**

    Pi is approximately 3.141590

**Note:** By default, `printf` outputs floating-point numbers with six
digits after the decimal. You can control this precision as shown below.

### 4. **Controlling Precision with `%f`** {#4-controlling-precision-with-f}

You can specify the number of digits after the decimal point by using
`%.Nf`, where `N` is the number of decimal places.

``` bash
printf "Pi to three decimal places: %.3f\n" 3.14159
```

**Output:**

    Pi to three decimal places: 3.142

### 5. **Hexadecimal Integer Specifier: `%x` and `%X`** {#5-hexadecimal-integer-specifier-x-and-x}

The `%x` specifier formats an integer as a hexadecimal number
(lowercase), and `%X` formats it as uppercase hexadecimal.

``` bash
printf "Lowercase hex: %x\n" 255
printf "Uppercase hex: %X\n" 255
```

**Output:**

    Lowercase hex: ff
    Uppercase hex: FF

### 6. **Octal Integer Specifier: `%o`** {#6-octal-integer-specifier-o}

The `%o` specifier formats an integer as an octal number.

``` bash
printf "Octal: %o\n" 8
```

**Output:**

    Octal: 10

### 7. **Character Specifier: `%c`** {#7-character-specifier-c}

The `%c` specifier formats an integer as the corresponding ASCII
character.

``` bash
printf "Character: %c\n" 65
```

**Output:**

    Character: A

### 8. **Width and Alignment** {#8-width-and-alignment}

You can control the width and alignment of your output using the `%N`
syntax, where `N` is the width.

-   **Right-aligned text with width 10:**

    ``` bash
    printf "%10s\n" "right"
    ```

    **Output:**

             right

-   **Left-aligned text with width 10 (using `-`):**

    ``` bash
    printf "%-10s\n" "left"
    ```

    **Output:**

        left      

### 9. **Zero-Padded Numbers** {#9-zero-padded-numbers}

You can pad numbers with leading zeros by using `%0Nd`, where `N` is the
total width including the zeros.

``` bash
printf "Zero-padded: %04d\n" 42
```

**Output:**

    Zero-padded: 0042

### 10. **Multiple Format Specifiers** {#10-multiple-format-specifiers}

You can combine multiple format specifiers in a single `printf`
statement.

``` bash
printf "Name: %s, Age: %d, GPA: %.2f\n" "Alice" 23 3.75
```

**Output:**

    Name: Alice, Age: 23, GPA: 3.75

### 11. **Percent Sign: `%%`** {#11-percent-sign-}

To print a literal percent sign, use `%%`.

``` bash
printf "Completion: 100%%\n"
```

**Output:**

    Completion: 100%

### 12. **Exponential Notation: `%e` and `%E`** {#12-exponential-notation-e-and-e}

The `%e` specifier formats numbers in scientific notation (lowercase
`e`), while `%E` uses an uppercase `E`.

``` bash
printf "Scientific notation: %e\n" 12345.6789
```

**Output:**

    Scientific notation: 1.234568e+04

### 13. **Handling Variable Lengths** {#13-handling-variable-lengths}

You can dynamically specify the width or precision by passing a `*`
instead of a number and providing the value as an additional argument.

-   **Variable width:**

    ``` bash
    width=10
    printf "%*s\n" $width "text"
    ```

    **Output:**

             text

-   **Variable precision:**

    ``` bash
    precision=2
    printf "%.*f\n" $precision 3.14159
    ```

    **Output:**

        3.14

These examples demonstrate the flexibility of the `printf` command in
Bash, allowing you to format text and numbers in various ways, similar
to how you would in C programming.
:::

::: {.cell .markdown}
# Examples Printing to a Variable

printf -v num4 \"%04d\" 4 printf \"%s\\n\" \"\$num4\"

Let\'s break down the two commands:

### 1. **Command: `printf -v num4 "%04d" 4`** {#1-command-printf--v-num4-04d-4}

#### Explanation:

-   **`printf`**: This is the command used to format and print data in a
    specified format.
-   **`-v num4`**: The `-v` option tells `printf` to assign the output
    to a variable instead of printing it to the standard output. In this
    case, the output is assigned to the variable `num4`.
-   **`"%04d"`**: This is the format specifier:
    -   **`%d`**: Specifies that the output should be an integer.
    -   **`04`**: Specifies that the output should be at least 4 digits
        wide and padded with leading zeros if necessary.
-   **`4`**: This is the integer value that you are formatting according
    to the format specifier.

#### Result:

-   The integer `4` will be formatted as `0004` (a 4-digit number with
    leading zeros) and assigned to the variable `num4`.

### 2. **Command: `printf "%s\n" "$num4"`** {#2-command-printf-sn-num4}

#### Explanation:

-   **`printf`**: Again, this is the command used to format and print
    data.
-   **`"%s\n"`**: This format specifier tells `printf` to print a string
    (`%s`) followed by a newline (`\n`).
-   **`"$num4"`**: This is the value of the variable `num4`, which is
    `0004`.

#### Result:

-   The command will print `0004` followed by a newline.

### Summary of Both Commands:

1.  The first command `printf -v num4 "%04d" 4` formats the number `4`
    to be 4 digits wide with leading zeros (`0004`) and stores the
    result in the variable `num4`.
2.  The second command `printf "%s\n" "$num4"` then prints the value of
    `num4`, which is `0004`, followed by a newline.

**Final Output:**

    0004
:::

::: {.cell .markdown}
Redirection in Bash allows you to control where input and output go,
enabling you to send the output of commands to files, read input from
files, or append data to files. Here's a breakdown of the redirection
operators `>`, `>>`, and `<`:

### 1. **Output Redirection: `>`** {#1-output-redirection-}

-   **Usage**: Redirects the standard output (stdout) of a command to a
    file. If the file already exists, it will be overwritten. If the
    file does not exist, it will be created.

-   **Example**:

    ``` bash
    echo "Hello, World!" > output.txt
    ```

    **Explanation**: The string `"Hello, World!"` is written to
    `output.txt`. If `output.txt` already exists, its contents will be
    replaced with `"Hello, World!"`.

-   **Effect**:

    -   If `output.txt` exists: The file\'s contents are overwritten.
    -   If `output.txt` does not exist: The file is created and the
        output is written to it.

### 2. **Append Redirection: `>>`** {#2-append-redirection-}

-   **Usage**: Redirects the standard output (stdout) of a command to a
    file, appending the output to the end of the file. If the file does
    not exist, it will be created.

-   **Example**:

    ``` bash
    echo "Hello, again!" >> output.txt
    ```

    **Explanation**: The string `"Hello, again!"` is appended to
    `output.txt`. If `output.txt` already exists, the content is added
    to the end of the file without altering the existing content. If
    `output.txt` does not exist, the file is created and the output is
    written to it.

-   **Effect**:

    -   If `output.txt` exists: The new output is appended to the end of
        the file.
    -   If `output.txt` does not exist: The file is created and the
        output is written to it.

### 3. **Input Redirection: `<`** {#3-input-redirection-}

-   **Usage**: Redirects the standard input (stdin) of a command from a
    file. This means that the command reads input from the specified
    file instead of from the keyboard or other standard input sources.

-   **Example**:

    ``` bash
    wc -l < input.txt
    ```

    **Explanation**: The `wc -l` command counts the number of lines in a
    file. Using `< input.txt`, the contents of `input.txt` are provided
    as input to `wc -l`. This is equivalent to running
    `wc -l input.txt`, but with the input provided via redirection.

-   **Effect**:

    -   The file `input.txt` is read and its contents are used as input
        for the command (`wc -l` in this example).

### Summary: {#summary}

-   **`>`**: Redirects stdout to a file, overwriting the file if it
    exists.
    -   **Example**: `echo "Hello" > file.txt` writes \"Hello\" to
        `file.txt`, replacing any existing content.
-   **`>>`**: Redirects stdout to a file, appending to the file if it
    exists.
    -   **Example**: `echo "Hello" >> file.txt` appends \"Hello\" to
        `file.txt`, preserving existing content.
-   **`<`**: Redirects stdin from a file, allowing a command to take
    input from the specified file instead of the keyboard.
    -   **Example**: `wc -l < file.txt` reads `file.txt` and counts its
        lines using `wc -l`.

These redirection operators are fundamental in shell scripting and
command-line operations, allowing you to manipulate data flow
efficiently.
:::

::: {.cell .markdown}
#Examples of Redirection printf \'%s\\n%v\\n\' OK? Oops! \> FILE 2\>
ERRORFILE printf \'%s\\n%v\\n\' OK? Oops! \> FILE 2\>&1

Let\'s break down the command you\'ve provided:

``` bash
printf '%s\n%v\n' OK? Oops! > FILE 2>&1
```

### Components of the Command:

1.  **`printf '%s\n%v\n' OK? Oops!`**:
    -   **`printf`**: A command used to format and print data.
    -   **`'%s\n%v\n'`**: The format string used by `printf`.
        -   **`%s`**: A format specifier for a string.
        -   **`\n`**: Represents a newline character.
        -   **`%v`**: **Note:** `%v` is not a standard format specifier
            in `printf`. Using `%v` will likely cause an error or
            produce unexpected output, as `printf` will not know how to
            interpret it.
    -   **`OK? Oops!`**: The strings that are being formatted and
        printed.
        -   **`OK?`** corresponds to `%s` in the format string.
        -   **`Oops!`** would correspond to `%v`, but as `%v` is not
            valid, this will cause an issue.
2.  **`> FILE`**:
    -   This redirects the standard output (stdout) of the `printf`
        command to a file named `FILE`. If `FILE` already exists, it
        will be overwritten. If it doesn\'t exist, it will be created.
3.  **`2>&1`**:
    -   This redirects the standard error (stderr) (file descriptor 2)
        to the same destination as standard output (file descriptor 1).
        Since stdout is already redirected to `FILE`, stderr will also
        be written to `FILE`.

### What Happens:

-   The `printf` command attempts to format and print the strings
    `"OK?"` and `"Oops!"` according to the format string `'%s\n%v\n'`.
-   Since `%v` is not a valid format specifier in Bash\'s `printf`, this
    will likely generate an error, which would normally be sent to
    stderr.
-   However, because of `2>&1`, both stdout and stderr are redirected to
    `FILE`.

### Expected Result:

1.  **`OK?`** will be printed as expected because `%s` is a valid format
    specifier.
2.  The command will likely produce an error due to the invalid `%v`
    format specifier.
3.  Both the successful output (`OK?`) and the error message related to
    `%v` will be written to `FILE`.

### Example Content of `FILE`:

Assuming an error is generated due to `%v`, the `FILE` might contain
something like:

    OK?
    bash: printf: %v: invalid format character

### Summary: {#summary}

-   The command attempts to print the strings `"OK?"` and `"Oops!"`
    using a format string.
-   The standard output and any error messages (due to the invalid `%v`
    format) are both redirected to a file named `FILE`.
-   The file `FILE` will contain the output `"OK?"` followed by an error
    message about the invalid `%v` specifier.
:::

::: {.cell .markdown}
In Bash, the `&>` operator is used to redirect both standard output
(stdout) and standard error (stderr) to a file. This is a shorthand for
combining the redirection of both stdout and stderr.

### Detailed Explanation:

-   **`&>`**: This is a redirection operator that sends both stdout and
    stderr to the specified destination. It\'s essentially a combination
    of `>` (for stdout) and `2>&1` (for stderr).

-   **`FILE`**: This is the destination file where both stdout and
    stderr will be redirected.

### How It Works:

When you use `&> FILE`, Bash does the following:

-   It redirects the output that would normally go to the terminal
    (stdout) to the specified `FILE`.
-   It also redirects any error messages (stderr) to the same `FILE`.

### Example: {#example}

``` bash
command &> output.txt
```

-   **`command`**: This is any command you want to run.
-   **`&> output.txt`**: This redirects both stdout and stderr of
    `command` to `output.txt`.

#### What happens: {#what-happens}

-   If `command` produces any regular output, it will be written to
    `output.txt`.
-   If `command` generates any errors, those error messages will also be
    written to `output.txt`.

### Example in Action:

Let\'s say you have a script or a command that produces both output and
errors:

``` bash
ls /nonexistent_directory &> output.txt
```

-   **Explanation**:

    -   The command `ls /nonexistent_directory` tries to list a
        directory that doesn\'t exist, which will produce an error.
    -   `&> output.txt` redirects both the error message and any
        potential output to `output.txt`.

-   **Content of `output.txt`** might look like this:

        ls: cannot access '/nonexistent_directory': No such file or directory

### Comparison with Other Redirections:

-   **`> FILE`**: Redirects only stdout to `FILE`, and stderr still goes
    to the terminal.
-   **`2> FILE`**: Redirects only stderr to `FILE`, and stdout still
    goes to the terminal.
-   **`&> FILE`**: Redirects both stdout and stderr to `FILE`.

### Summary: {#summary}

-   **`&> FILE`** is a convenient way to redirect both the standard
    output and standard error of a command to a single file.
-   This ensures that all output, whether successful or error messages,
    is captured in the specified file, making it easier to log and
    debug.
:::

::: {.cell .markdown}
In Bash, the `2>&1` construct is used for redirection, specifically to
redirect the standard error (stderr) to the same location as the
standard output (stdout). Let\'s break this down:

### Components:

1.  **`2`**:
    -   This refers to file descriptor `2`, which is the standard error
        (stderr) in Unix-like operating systems.
2.  **`>`**:
    -   This is the redirection operator. It redirects the output of a
        file descriptor to another file or file descriptor.
3.  **`&1`**:
    -   The `&` symbol indicates that what follows is a file descriptor,
        not a file name.
    -   `1` is the file descriptor for standard output (stdout).

### How It Works: {#how-it-works}

-   **`2>&1`** tells the shell to redirect the standard error (file
    descriptor `2`) to wherever the standard output (file descriptor
    `1`) is currently being redirected.

### Use Cases:

-   **Capturing both stdout and stderr**: When you want to capture both
    standard output and standard error in the same file or pipe them
    into another command, you use `2>&1`.

### Examples:

1.  **Redirecting both stdout and stderr to a file**:

    ``` bash
    command > output.txt 2>&1
    ```

    -   **`command > output.txt`**: Redirects stdout to `output.txt`.
    -   **`2>&1`**: Redirects stderr to the same place stdout is going
        (i.e., `output.txt`).

    **Result**: Both stdout and stderr of `command` are written to
    `output.txt`.

2.  **Piping both stdout and stderr to another command**:

    ``` bash
    command 2>&1 | another_command
    ```

    -   **`command`**: The command whose output you want to process.
    -   **`2>&1`**: Redirects stderr to stdout.
    -   **`| another_command`**: Pipes the combined stdout and stderr to
        `another_command`.

    **Result**: Both the standard output and error of `command` are
    processed by `another_command`.

### Example in Action: {#example-in-action}

Suppose you have a command that produces both output and an error:

``` bash
ls /nonexistent_directory /tmp 2>&1
```

-   **Explanation**:
    -   `ls /nonexistent_directory /tmp` tries to list both a
        nonexistent directory and `/tmp`.
    -   The output for `/tmp` will go to stdout.
    -   The error message for `/nonexistent_directory` will go to
        stderr.
    -   **`2>&1`** redirects stderr to wherever stdout is going.

### Summary: {#summary}

-   **`2>&1`** is used to redirect stderr (file descriptor `2`) to the
    same location as stdout (file descriptor `1`).
-   This is useful for combining both standard output and standard error
    into a single stream, whether you\'re writing them to a file, piping
    them to another command, or processing them together in some way.
:::

::: {.cell .markdown}
In Bash, reading input from the user or from files is a common task,
often accomplished using the `read` command and other input-handling
techniques. Here's a detailed explanation of how to read input in Bash:

### 1. **Reading Input from the User with `read`** {#1-reading-input-from-the-user-with-read}

The `read` command is used to take input from the user or from a file.
It reads a line of input and assigns it to one or more variables.

#### Basic Usage:

``` bash
read variable
```

-   **Example**:

    ``` bash
    echo "Enter your name:"
    read name
    echo "Hello, $name!"
    ```

    **What Happens**:

    -   The script prompts the user with \"Enter your name:\".
    -   It waits for the user to input their name and press `Enter`.
    -   The input is stored in the variable `name`.
    -   The script then prints \"Hello, `name`!\", using the input
        provided by the user.

#### Reading Multiple Variables:

``` bash
read var1 var2 var3
```

-   **Example**:

    ``` bash
    echo "Enter three values:"
    read a b c
    echo "You entered: $a, $b, $c"
    ```

    **What Happens**:

    -   The user is prompted to enter three values separated by spaces.
    -   The first value is assigned to `a`, the second to `b`, and the
        third to `c`.
    -   The script then prints out the values entered.

### 2. **Using `read` with Options** {#2-using-read-with-options}

The `read` command has several useful options that can change its
behavior:

-   **`-p`**: Prompt the user with a message.

    ``` bash
    read -p "Enter your name: " name
    echo "Hello, $name!"
    ```

    **This is a shortcut for combining `echo` and `read` in one step.**

-   **`-s`**: Silent mode (does not echo input). Useful for passwords.

    ``` bash
    read -sp "Enter your password: " password
    echo
    echo "Password entered."
    ```

    **What Happens**:

    -   The input is not displayed as the user types (useful for
        sensitive information like passwords).

-   **`-t`**: Timeout after a certain number of seconds.

    ``` bash
    if read -t 5 -p "Enter your name within 5 seconds: " name; then
        echo "Hello, $name!"
    else
        echo "Time's up!"
    fi
    ```

    **What Happens**:

    -   The script waits for 5 seconds for user input. If no input is
        provided within the timeout, it prints \"Time\'s up!\".

-   **`-n`**: Limit the input to a certain number of characters.

    ``` bash
    read -n 1 -p "Press any key to continue..."
    ```

    **What Happens**:

    -   The script waits for the user to press a single key before
        continuing.

-   **`-r`**: Prevents backslashes from escaping characters (useful for
    reading file paths or raw input).

    ``` bash
    read -r filepath
    echo "You entered: $filepath"
    ```

    **What Happens**:

    -   Backslashes are treated as literal characters rather than escape
        characters.

### 3. **Reading Input from a File** {#3-reading-input-from-a-file}

You can read input from a file line by line using a `while` loop
combined with `read`.

-   **Example**:

    ``` bash
    while IFS= read -r line; do
        echo "Line: $line"
    done < input.txt
    ```

    **Explanation**:

    -   **`IFS=`**: Sets the Internal Field Separator to an empty value
        to preserve leading/trailing whitespace.
    -   **`read -r line`**: Reads each line from the file without
        interpreting backslashes.
    -   **`< input.txt`**: Redirects the content of `input.txt` to the
        `while` loop.

    **What Happens**:

    -   Each line of `input.txt` is read and stored in the variable
        `line`, then printed out.

### 4. **Reading Input from a Command** {#4-reading-input-from-a-command}

You can use command substitution to read input from the output of a
command.

-   **Example**:

    ``` bash
    read current_user <<< "$(whoami)"
    echo "Current user is $current_user"
    ```

    **Explanation**:

    -   The output of the `whoami` command is assigned to the variable
        `current_user`.

### 5. **Handling User Input with Defaults** {#5-handling-user-input-with-defaults}

You can provide a default value for a variable if the user does not
input anything.

-   **Example**:

    ``` bash
    read -p "Enter your name [Default: John]: " name
    name=${name:-John}
    echo "Hello, $name!"
    ```

    **Explanation**:

    -   If the user presses Enter without typing anything, `name` will
        be set to \"John\" by default.

### Summary: {#summary}

-   **`read`**: The primary command for reading input in Bash, whether
    from the user or from files.
-   **Options**: `-p` for prompts, `-s` for silent input, `-t` for
    timeouts, `-n` for character limits, `-r` for raw input.
-   **File Input**: Use `while` loops to read from files.
-   **Command Input**: Use command substitution to capture the output of
    commands.
-   **Defaults**: Handle empty input with default values.

These techniques allow you to effectively manage input in Bash scripts
for a variety of use cases.
:::

::: {.cell .markdown}
Piping in Bash is a powerful feature that allows you to take the output
of one command and use it as the input for another command. This is done
using the pipe operator (`|`). Piping is a fundamental concept in
Unix-like operating systems and enables you to chain commands together
to perform complex tasks in a streamlined manner.

### Basic Concept of Piping

The pipe operator (`|`) connects the standard output (stdout) of one
command to the standard input (stdin) of another command. This means
that whatever data is produced by the first command is immediately fed
as input to the second command.

### Syntax

``` bash
command1 | command2 | command3
```

-   **`command1`**: The first command in the pipeline, which produces
    output.
-   **`|`**: The pipe operator, which passes the output of `command1` to
    `command2`.
-   **`command2`**: The second command, which takes the output of
    `command1` as its input.

### Examples {#examples}

#### 1. **Using `ls` and `grep`** {#1-using-ls-and-grep}

List all files in the current directory and then filter out only the
ones that contain the string \"log\":

``` bash
ls | grep log
```

-   **`ls`**: Lists the files and directories.
-   **`| grep log`**: Filters the list to show only those entries
    containing \"log\".

#### 2. **Using `cat`, `grep`, and `wc`** {#2-using-cat-grep-and-wc}

Count the number of lines in a file that contain a specific word:

``` bash
cat file.txt | grep "search_term" | wc -l
```

-   **`cat file.txt`**: Outputs the contents of `file.txt`.
-   **`| grep "search_term"`**: Filters the output to include only lines
    containing \"search_term\".
-   **`| wc -l`**: Counts the number of lines that contain
    \"search_term\".

#### 3. **Using `ps` and `grep`** {#3-using-ps-and-grep}

Find out if a specific process is running:

``` bash
ps aux | grep "process_name"
```

-   **`ps aux`**: Lists all running processes.
-   **`| grep "process_name"`**: Filters the list to show only lines
    containing \"process_name\".

### Combining Multiple Commands

Pipes can be used to combine more than two commands. For instance:

``` bash
cat file.txt | grep "error" | sort | uniq -c | sort -nr
```

-   **`cat file.txt`**: Outputs the contents of `file.txt`.
-   **`grep "error"`**: Filters lines that contain \"error\".
-   **`sort`**: Sorts the filtered lines.
-   **`uniq -c`**: Counts the occurrences of each unique line.
-   **`sort -nr`**: Sorts the counts in numerical order, highest to
    lowest.

### Advantages of Piping

-   **Efficiency**: Piping allows you to perform complex tasks in a
    single line of commands without the need to create temporary files.
-   **Simplicity**: It simplifies workflows by chaining together
    commands that handle different parts of a task.
-   **Modularity**: You can build powerful command chains by combining
    simple, single-purpose tools.

### Common Use Cases

1.  **Data Processing**: Filter and process text data, like logs, with
    commands such as `grep`, `awk`, `sed`, and `cut`.
2.  **System Administration**: Combine commands like `ps`, `top`,
    `grep`, and `kill` to manage processes.
3.  **File Manipulation**: Use `find`, `xargs`, `grep`, and `awk` to
    locate and process files in bulk.

### Things to Keep in Mind

-   **Order Matters**: The order of commands in a pipeline is crucial
    since the output of one command becomes the input of the next.
-   **Resource Use**: Each command in a pipeline runs as a separate
    process, so complex pipelines can be resource-intensive.
-   **Error Handling**: Piping handles only stdout. If you need to
    handle stderr (error messages), you may need to redirect it
    explicitly using `2>&1` or similar constructs.

### Summary {#summary}

Piping in Bash is a powerful feature that allows you to chain together
commands, making the output of one command the input for another. This
enables efficient and streamlined data processing, system
administration, and file manipulation. By understanding and leveraging
pipes, you can perform complex tasks with simple, modular commands,
enhancing both your productivity and the clarity of your scripts.
:::

::: {.cell .markdown}
The `tee` command in Bash is used to read from standard input (stdin)
and write the input to both standard output (stdout) and one or more
files. Essentially, it allows you to \"tee\" (split) the input so that
you can see the output on the screen while simultaneously saving it to a
file or multiple files.

### Syntax {#syntax}

``` bash
command | tee [OPTION]... [FILE]...
```

-   **`command`**: The command whose output you want to process.
-   **`|`**: The pipe operator, which passes the output of `command` to
    `tee`.
-   **`tee [FILE]...`**: Writes the output to the specified files and
    also passes it through to stdout.

### How `tee` Works

1.  **Reads input from stdin**: The `tee` command reads data passed to
    it through a pipe.
2.  **Writes to stdout**: It outputs this data to the terminal (stdout),
    so you can see it.
3.  **Writes to one or more files**: It also writes the same data to one
    or more specified files.

### Common Options

-   **`-a` or `--append`**: Appends the output to the file(s) instead of
    overwriting them.

    ``` bash
    command | tee -a file.txt
    ```

    This appends the output of `command` to `file.txt` without
    overwriting existing content.

-   **`-i` or `--ignore-interrupts`**: Ignores interrupt signals (e.g.,
    `CTRL+C`), which allows `tee` to complete its operation even if an
    interrupt is sent.

### Examples {#examples}

#### 1. **Basic Use of `tee`** {#1-basic-use-of-tee}

Let\'s say you want to list all files in the current directory and save
the output to a file while still seeing the output on the screen:

``` bash
ls -l | tee output.txt
```

-   **Explanation**:
    -   `ls -l` lists the files in the directory with details.
    -   `| tee output.txt` writes the output to `output.txt` and also
        displays it on the screen.

**Output** (on the screen and in `output.txt`):

    total 4
    -rw-r--r-- 1 user user  0 Aug 23 12:34 file1
    -rw-r--r-- 1 user user  0 Aug 23 12:34 file2

#### 2. **Appending to a File** {#2-appending-to-a-file}

To append the output to an existing file rather than overwriting it:

``` bash
ls -l | tee -a output.txt
```

-   **Explanation**:
    -   The `-a` option tells `tee` to append the output to `output.txt`
        rather than overwriting it.

#### 3. **Writing to Multiple Files** {#3-writing-to-multiple-files}

You can write the output to multiple files by specifying more than one
file name:

``` bash
ls -l | tee output1.txt output2.txt
```

-   **Explanation**:
    -   This command writes the output of `ls -l` to both `output1.txt`
        and `output2.txt`, as well as displaying it on the screen.

#### 4. **Using `tee` with `sudo`** {#4-using-tee-with-sudo}

Sometimes you need to write output to a file that requires elevated
permissions, but you still want to see the output on the screen. `tee`
is useful for this:

``` bash
echo "New configuration" | sudo tee /etc/someconfigfile
```

-   **Explanation**:
    -   `echo "New configuration"` produces some text.
    -   `| sudo tee /etc/someconfigfile` writes the text to
        `/etc/someconfigfile` using `sudo` to gain the necessary
        permissions, while also displaying it on the screen.

#### 5. **Combining `tee` with Other Commands** {#5-combining-tee-with-other-commands}

You can combine `tee` with commands like `grep` to save filtered output:

``` bash
grep "search_term" file.txt | tee result.txt
```

-   **Explanation**:
    -   `grep "search_term" file.txt` searches for \"search_term\" in
        `file.txt`.
    -   `| tee result.txt` writes the matching lines to `result.txt` and
        displays them on the screen.

### Summary {#summary}

-   **`tee`** is a command used to split the output of a command so that
    it can be simultaneously written to one or more files and displayed
    on the screen.
-   **Common Use Cases**:
    -   Saving command output to a file while still seeing it on the
        screen.
    -   Appending output to an existing file.
    -   Writing output to multiple files at once.
-   **Important Options**:
    -   `-a` for appending to files.
    -   `-i` for ignoring interrupts.

`tee` is particularly useful in scripts or during command-line work
where you need to monitor output in real-time while also logging it to a
file.
:::

::: {.cell .markdown}
Command substitution in Bash is a powerful feature that allows you to
capture the output of a command and use it as input or as a value within
your script. This can be used to assign the output of a command to a
variable, pass it as an argument to another command, or even embed it
directly within a string.

### Basic Syntax {#basic-syntax}

There are two common syntaxes for command substitution in Bash:

1.  **Using backticks (`` `command` ``)**:

    ``` bash
    result=`command`
    ```

2.  **Using `$(command)` (recommended)**:

    ``` bash
    result=$(command)
    ```

### Why Use `$(command)` Over Backticks?

-   **Readability**: The `$(command)` syntax is more readable,
    especially when commands are nested.
-   **Nestability**: You can easily nest commands using `$(command)`,
    while with backticks, it can become confusing and error-prone.

### Examples of Command Substitution

#### 1. **Assigning Command Output to a Variable** {#1-assigning-command-output-to-a-variable}

You can store the output of a command in a variable:

``` bash
current_date=$(date)
echo "Today's date is: $current_date"
```

-   **Explanation**:
    -   `$(date)` runs the `date` command and captures its output.
    -   The output is stored in the `current_date` variable.
    -   `echo` prints the value of `current_date`.

**Output**:

    Today's date is: Thu Aug 23 14:45:00 UTC 2024

#### 2. **Using Command Output in a String** {#2-using-command-output-in-a-string}

You can embed the output of a command directly within a string:

``` bash
echo "The current directory is $(pwd)"
```

-   **Explanation**:
    -   `$(pwd)` captures the output of the `pwd` command, which prints
        the current directory.
    -   The output is embedded directly within the string.

**Output**:

    The current directory is /home/user

#### 3. **Using Command Output as Arguments** {#3-using-command-output-as-arguments}

You can pass the output of a command as an argument to another command:

``` bash
files=$(ls *.txt)
tar -czf archive.tar.gz $files
```

-   **Explanation**:
    -   `$(ls *.txt)` captures the list of `.txt` files in the current
        directory.
    -   The list of files is passed as arguments to the `tar` command to
        create an archive.

#### 4. **Nesting Commands** {#4-nesting-commands}

You can nest command substitutions to perform more complex tasks:

``` bash
result=$(echo $(date +%Y) is the year)
echo $result
```

-   **Explanation**:
    -   The inner `$(date +%Y)` gets the current year.
    -   The outer `$(echo $(date +%Y) is the year)` forms a complete
        sentence, capturing it in `result`.

**Output**:

    2024 is the year

### Common Use Cases {#common-use-cases}

-   **Dynamic Filenames**:
    -   Create filenames that include dynamic content, such as the
        current date or user input.

    ``` bash
    filename="backup_$(date +%Y%m%d).tar.gz"
    ```
-   **Inline Calculations**:
    -   Perform arithmetic or other calculations on the fly.

    ``` bash
    result=$((5 + 3))
    echo "The result is $result"
    ```
-   **System Information**:
    -   Quickly gather system information and store it in variables.

    ``` bash
    kernel_version=$(uname -r)
    echo "Running kernel version: $kernel_version"
    ```

### Command Substitution with Multiple Lines

If the output of the command spans multiple lines, you can still capture
it:

``` bash
files=$(ls)
echo "Files in the current directory:"
echo "$files"
```

-   **Explanation**:
    -   `$(ls)` captures the list of files, which may span multiple
        lines.
    -   The entire output is stored in `files` and can be printed as-is.

### Combining Command Substitution with Loops and Conditionals

Command substitution is often used within loops or conditionals to make
decisions based on command output:

``` bash
if [ "$(whoami)" = "root" ]; then
    echo "You are root"
else
    echo "You are not root"
fi
```

-   **Explanation**:
    -   `$(whoami)` captures the current username.
    -   The `if` statement checks if the user is `root` and prints an
        appropriate message.

### Summary {#summary}

-   **Command substitution** allows you to capture the output of a
    command and use it within your script or command line.
-   **Syntax**: Use `$(command)` (recommended) or backticks
    (`` `command` ``) for command substitution.
-   **Use Cases**: Assigning command output to variables, embedding
    command output within strings, passing output as arguments,
    performing calculations, and more.
-   **Readability**: Prefer `$(command)` over backticks for better
    readability and easier nesting.

By mastering command substitution, you can make your Bash scripts more
dynamic and powerful, leveraging the full capabilities of the shell.
:::

::: {.cell .markdown}
Check on learning:
:::

::: {.cell .markdown}
Example: tr A Z \< \$HOME/temp \> \$HOME/temp
:::

::: {.cell .markdown}
SED vs TR in Bash In Bash, both `sed` and `tr` are powerful text
processing tools, but they serve different purposes and are used in
different contexts. Here\'s a comparison of the two, including when to
use each:

### **`sed` (Stream Editor)**

`sed` is a powerful stream editor that is used for processing and
transforming text in various ways. It can perform more complex text
manipulations than `tr`, including:

-   **Substitution**: Replace occurrences of patterns with different
    text.
-   **Deletion**: Remove lines or parts of lines that match a pattern.
-   **Insertion**: Add new text at specific locations.
-   **Transformation**: Similar to `tr`, but usually for more complex or
    multi-line patterns.
-   **In-place Editing**: Modify files directly without the need for
    intermediate files (using the `-i` option).

#### **Common Use Cases:** {#common-use-cases}

1.  **Substituting Text**:

    ``` bash
    sed 's/oldtext/newtext/' file.txt
    ```

    -   Replaces the first occurrence of \"oldtext\" with \"newtext\" in
        each line.

2.  **Deleting Lines**:

    ``` bash
    sed '/pattern/d' file.txt
    ```

    -   Deletes lines that match the \"pattern\".

3.  **In-Place Editing**:

    ``` bash
    sed -i 's/oldtext/newtext/' file.txt
    ```

    -   Replaces \"oldtext\" with \"newtext\" directly in `file.txt`.

4.  **Advanced Pattern Matching**:

    ``` bash
    sed -n '/startpattern/,/endpattern/p' file.txt
    ```

    -   Prints lines between \"startpattern\" and \"endpattern\".

#### **Advantages of `sed`:**

-   **Versatility**: `sed` can handle a wide range of text processing
    tasks, from simple substitutions to complex multi-line edits.
-   **Pattern Matching**: Uses regular expressions, allowing for complex
    search-and-replace operations.
-   **In-Place Editing**: Modify files directly without the need to
    create temporary files.

### **`tr` (Translate or Delete Characters)**

`tr` is a more specialized tool that is used primarily for
character-by-character transformations. It cannot match patterns or
manipulate text in complex ways like `sed`, but it is very efficient for
tasks that involve:

-   **Character Translation**: Replace specific characters with others.
-   **Character Deletion**: Remove specific characters from the input.
-   **Character Compression**: Remove repeated characters.

#### **Common Use Cases:** {#common-use-cases-1}

1.  **Character Translation**:

    ``` bash
    echo "hello" | tr 'a-z' 'A-Z'
    ```

    -   Converts all lowercase letters to uppercase.

2.  **Character Deletion**:

    ``` bash
    echo "hello123" | tr -d '0-9'
    ```

    -   Removes all digits from the input.

3.  **Character Compression**:

    ``` bash
    echo "hellooo    world" | tr -s 'o' ' '
    ```

    -   Squeezes repeated characters (e.g., multiple spaces into a
        single space).

#### **Advantages of `tr`:**

-   **Simplicity**: Ideal for simple, single-character transformations
    and deletions.
-   **Efficiency**: Faster and more straightforward for tasks that match
    its capabilities.

### **When to Use `sed` vs. `tr`** {#when-to-use-sed-vs-tr}

-   **Use `sed` when**:
    -   You need to work with patterns or regular expressions.
    -   You need to manipulate lines of text (e.g., inserting, deleting,
        or substituting entire lines or sections).
    -   You need to perform in-place editing of files.
    -   You need to perform multi-line operations or more complex text
        transformations.
-   **Use `tr` when**:
    -   You need to transform individual characters or sets of
        characters.
    -   You need to delete specific characters.
    -   You need to compress sequences of repeated characters.
    -   You are performing simple transformations that don\'t require
        pattern matching or complex logic.

### **Examples of `sed` vs. `tr`** {#examples-of-sed-vs-tr}

1.  **Case Conversion**:
    -   Using `tr`:

        ``` bash
        echo "hello world" | tr 'a-z' 'A-Z'
        ```

    -   Using `sed`:

        ``` bash
        echo "hello world" | sed 'y/abcdefghijklmnopqrstuvwxyz/ABCDEFGHIJKLMNOPQRSTUVWXYZ/'
        ```
2.  **Replacing Text**:
    -   Using `sed` (you can\'t do this with `tr`):

        ``` bash
        echo "hello world" | sed 's/hello/hi/'
        ```
3.  **Removing Digits**:
    -   Using `tr`:

        ``` bash
        echo "abc123def" | tr -d '0-9'
        ```

    -   Using `sed`:

        ``` bash
        echo "abc123def" | sed 's/[0-9]//g'
        ```

### **Summary** {#summary}

-   **`sed`** is a versatile stream editor that handles complex text
    processing tasks, making it ideal for line-based transformations and
    regular expression-based substitutions.
-   **`tr`** is a simpler tool designed for straightforward character
    transformations, deletions, and compressions, making it more
    efficient for these specific tasks.

Choose the tool that best fits the complexity and nature of the task
you\'re trying to accomplish.
:::

::: {.cell .markdown}
TASK:
:::

::: {.cell .markdown}
Write a bash script using \$RANDOM to write the following output both to
a file and to a variable. The following numbers are only to show the
format; your script should produce different numbers: 1988.2345
13798.12343 10081.134 3816.15098
:::

::: {.cell .markdown}
Here's a Bash script that generates random numbers using `$RANDOM`,
formats them to the desired precision, and writes the output both to a
file and to a variable. The script will generate four random numbers in
the format you provided and store them in a variable as well as write
them to a file.

### Script: `generate_random_numbers.sh` {#script-generate_random_numberssh}

``` bash
#!/bin/bash

# File to store the output
output_file="random_numbers.txt"

# Initialize an empty variable to store the output
random_numbers=""

# Function to generate a random number with a decimal point
generate_random_number() {
  integer_part=$(($RANDOM + 1000))       # Ensures the integer part is at least 1000
  decimal_part=$(($RANDOM % 100000))    # Generates a decimal part with up to 5 digits
  echo "$integer_part.$decimal_part"
}

# Generate four random numbers and store them in the variable and file
for i in {1..4}; do
  random_number=$(generate_random_number)
  random_numbers+="$random_number"$'\n'  # Add to the variable with a newline
done

# Write the output to the file
echo "$random_numbers" > "$output_file"

# Display the output stored in the variable
echo "Generated random numbers:"
echo "$random_numbers"

# Inform the user where the output has been stored
echo "The random numbers have been saved to $output_file"
```

### Explanation: {#explanation}

1.  **`generate_random_number()` Function**:
    -   This function generates a random integer part and a random
        decimal part.
    -   `integer_part=$(($RANDOM + 1000))` ensures that the integer part
        of the number is at least 1000.
    -   `decimal_part=$(($RANDOM % 100000))` generates a decimal part
        with up to 5 digits.
    -   The function then concatenates the integer and decimal parts to
        form a random number in the desired format.
2.  **Loop to Generate Numbers**:
    -   The `for i in {1..4}` loop generates four random numbers by
        calling the `generate_random_number` function.
    -   Each number is added to the `random_numbers` variable, with a
        newline character separating each entry.
3.  **Writing to File and Variable**:
    -   The `random_numbers` variable, which now contains all four
        generated numbers, is written to `output_file` using `echo`.
    -   The script also prints the generated numbers to the screen.

### Running the Script:

Save the script to a file named `generate_random_numbers.sh`, make it
executable, and run it:

``` bash
chmod +x generate_random_numbers.sh
./generate_random_numbers.sh
```

### Example Output:

Running the script might produce output similar to this:

    Generated random numbers:
    11577.45679
    17427.9827
    14230.37421
    13918.1202

    The random numbers have been saved to random_numbers.txt

-   The numbers generated will be different each time you run the script
    due to the use of `$RANDOM`.
:::
