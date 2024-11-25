# **Ch2**: Key Concepts
- Moving around and listing files/directories so you know where you're at.
- Introduction to hidden files

# **Ch2**: Summarization
- The first directory (same thing as "folder"), is the root directory, denoted by a single slash "/"
- Directories within directories are targeted by a slash count.
- /first/second/third/fourth/target would be an example of an absolute path where we start at root /
- Directories with relative paths are denoted with either the assumed current directory denoted by a single dot `.` or can be used to move back a directory with a double dot `..`
- `.` notation refers to the current working directory. In almost all cases you can omit the `./` because it is assumed/implied by the system.
- `..` refers to the previous/parent directory in the chain
- Filenames beginning with a dot are hidden. Ex: `.hidden` would be hidden regardless if it was a directory or file.
- Filenames, directories, and commands are case sensitive. Type with intention!

## Commands
- `pwd` - prints the current working directory.
- `ls` - lists a directories contents (i.e. more directories or files). By default it assumes the current directory, but a relative/absolute path may be specified.
- `cd` - used to change directories with a relative/absolute path.

`cd` shortcuts:

| Shortcut | Results |
| -------- | ------- |
`cd` | `cd` to your home directory 
`cd -` | `cd` to the previous directory
`cd ~user_name` | `cd` to ~bob's home directory.

# **Ch2**: Thoughts
- You can't help people to go anywhere if you don't know where you are.
