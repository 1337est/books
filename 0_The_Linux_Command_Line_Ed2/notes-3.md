# **Ch3**: Key Concepts
- There's more to commands than meets the eye.
- File structure is important and understanding it helps to understand your system.

# **Ch3**: Summarization
- Options and arguments are used in conjunction with commands to have varied output/behavior.
- Options modify the behavior/output
- Arguments specify what you want to modify/act onto.
- A core concept, or way of thinking, for Unix-like operating systems is "EVERYTHING is a file".
- To get a rundown of the linux Filesystem Hierarchy Standard, use `man hier`.
- Symbolic links allow for the same file to be located in multiple locations, with different names, but are essentially identical. Similar to copy, but if the symbolically linked file is modified, so is the other side of the node. They are entangled.

## Commands
- `ls` - lists files/directories for the given path
- `file` - prints a description of the file's type and file information
- `less` - view a file's contents, with ability to scroll up and down. The `man` command uses `less` by default to read documentation/manual pages. To exit the `less` program, press 'q'.

# **Ch3**: Code Snippets
There are options and arguments that generally come with commands. To learn specific ones use `man "command"`. Although the format is generally:
```bash
command -options arguments
```
this is not always the case since -options can follow after the command or arguments and arguments can follow after the commands or options depending on the context of the command/option/arugment. This is why it's vital to read the documentation for the command.
 
Here the command is `ls` the option is `-l` and the argument is the parent/previous directory `../`
```bash
ls -l ../
```
