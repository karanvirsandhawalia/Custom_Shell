mysh - A Custom Unix Shell
A feature-rich Unix shell in C with built-in commands, variables, pipes, background processes, and TCP chat.
Built-in Commands
CommandUsageDescriptionechoecho [args...]Print arguments separated by spacescdcd <path>Change directory (supports ., .., relative, absolute)lsls [path] [--rec] [--d <depth>] [--f <substring>]List directory contents with optional recursion, depth limit, and filteringcatcat [file]Display file contents or read stdinwcwc [file]Count words, characters, and linespspsList background processeskillkill <pid> [signal]Kill a process (default: SIGTERM)exitexitExit the shell
Shell Variables
Define variables with var=value and expand with $var:
mysh$ greeting=hello
mysh$ echo $greeting
hello
Pipes
Chain commands with |:
mysh$ cat file.txt | wc
mysh$ echo hello | cat
Background Processes
Run commands with &:
mysh$ long_running_command &
[1] 12345
Returns immediately to the prompt.
TCP Chat System
CommandUsageDescriptionstart-serverstart-server <port>Start a chat serverclose-serverclose-serverShut down the serverstart-clientstart-client <port> <host>Connect as a clientsendsend <port> <host> <message>Send a one-off message
In client mode, type \connected to see active connections.
Build & Run
bashmake              # Compile
make clean        # Clean artifacts
./mysh            # Run
Signal Handling
SignalBehaviorCtrl+CRedisplay prompt (don't exit)Ctrl+DExit gracefullySIGTERM/SIGHUPClean shutdown with server cleanupSIGCHLDAuto-reap background processes
ls Options
mysh$ ls                        # Current directory
mysh$ ls /home                  # Specific directory
mysh$ ls --rec                  # Recursive (unlimited depth)
mysh$ ls --rec --d 2            # Recursive with max depth 2
mysh$ ls --f .txt               # Filter files by substring
mysh$ ls --rec --d 3 --f test   # Combine options
Project Structure
├── mysh.c              # Main shell loop
├── builtins.c/h        # Built-in commands
├── commands.c/h        # Server/client commands
├── client_manager.c/h  # TCP socket management
├── variables.c/h       # Variable storage & expansion
├── io_helpers.c/h      # I/O utilities & tokenization
└── Makefile
Limits

Input line: 128 chars max
Chat username: 10 chars max
Chat message: 129 chars max
Background processes: Up to 1000 PIDs

Requirements

GCC
POSIX system (Linux/macOS)
Standard C libraries

License
Educational purposes.
