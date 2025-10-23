##
## How it works (for programmers)
- creates a TCP socket (`AF_INET`, `SOCK_STREAM`)  
- attempts `connect()` to `127.0.0.1:4444` in a loop  
- on success `fork()`s; the child `dup2()`s the socket to fd 0/1/2 and `execve("/bin/sh", ...)`  
- parent closes the socket and `wait()`s for the child, then continues looping
##
## What it does (plain English for non programmers) 
- Opens a network connection to `127.0.0.1` on port `4444`.  
- Keeps trying to connect in evry 3 sec until the connection succeeds.  
- When connected, it starts a shell (`/bin/sh`) and hooks the shell’s keyboard input and output to that network connection so the other end can type commands and see results.  
- After the shell exits it closes the connection and keeps trying to cnonect in every 3 sec very presistence...
