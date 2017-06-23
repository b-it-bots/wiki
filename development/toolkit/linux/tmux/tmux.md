# TMUX - Terminal Multiplexer

## Full Documentation
- [Project page](https://tmux.github.io/)
- [Manual Page](http://man.openbsd.org/OpenBSD-current/man1/tmux.1)

## Why tmux
- Allow starting process in `ssh` sessions that continue to run when the user logout
- Open the same session on multiple computers
- Hide irrelevant sessions to unclutter the terminal
- and many others...

## Essential Usage
### In the terminal
- Start a new session: `tmux new -s <session_name>`
- List sessions: `tmux ls`
- Attach to an existing session: `tmux attach -t <session_name>`

### Within a session
The default bind key for tmux is `C-b` (`Ctrl+b`)
- `C-b + d`: detach (session run as background)
- `C-d` : exit (kill session), typing `exit` on all terminals also work
- `C-b + %`: vertical split
- `C-b + "`: horizontal split
- `C-b + :`: enter command
- `C-b + [`: enter scroll/copy mode
- `Esc` or `q`: exit scroll/copy mode

## (More) Advanced Usage
An user-specific config file for tmux should be located at `~/.tmux.conf`
- Enable scrolling by default: enter following command or add it to config file:
  - version 2.1 and up: `set -g mouse on`
  - older versions: `set -g mode-mouse on`

## See also
* https://egghead.io/courses/wrangle-your-terminal-with-tmux
