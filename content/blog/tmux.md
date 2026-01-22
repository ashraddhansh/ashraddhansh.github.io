+++
title = "Tmux"
date = 2019-11-27
+++

**tmux is a terminal multiplexer tool**

# How to install
```bash
sudo pacman -S tmux
```

# How to launch
```bash
tmux
```

this will open a new tmux window with a footer at bottom.

# How to detach from tmux session
Press CTRL+B to enter tmux command mode then  press  'd' to detach from that window and back to normal terminal.

By using this we can run multiple processes at once.

# How to go back to most recent tmux session
```bash
tmux attach
```

# How to list all the running tmux session
```bash
tmux list-sessions
```

or 
```bash
tmux ls
```

# How to exit a tmux sessions
type exit on that session to exit from that

```bash
exit
```

or
Go to command mode then press x then press y.
# How to detach from tmux session
go to command mode and then press D to detach from the session.


# How to vertically split tmux panes
- Go to command mode by pressing CTRL+B then press `%`

# How to horizontally split tmux panes
- Go to command mode by pressing CTRL+B then  press `"`

# How to change focus between multiple tmux panes
Press left, right, top, bottom arrow keys to move focus to left, right, top and bottom panes respectively.


![image](/images/tmux.png)

# How to create a new window in tmux
```bash
tmux new-window
```

or
Press leader key then `c`  to create a new window.

# How to navigate between windows
 Press `n`  or `p`  followed by leader key to navigate to next and previous window.

# How to kill a tmux window
Press `&`  followed by leader key to kill the active window.
Or
```bash
tmux kill-window
```
in that window you want to kill.

# How to rename a tmux window
Press `,`  followed by leader key to rename a window.
 Or
 ```bash
 tmux rename-window 'new name'
```
# How to rename a session
Press `$` followed by leader key to rename a session.
