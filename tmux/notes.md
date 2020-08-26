# tmux (Room 003)

# About

## tmux is a terminal multiplexer. Makes running simulatenous tasks easy

![](/images/tmux_cheat_sheet.png)

## Installing tmux

To install on Ubuntu/Kali, use `apt-get install tmux` command

## New Session

To launch a new session without a name, use the `tmux` command. Default session name is 0

## Commands

All tmux commands start with Ctrl+B prefix

## Detaching

To detach from a session, use `CtrlB + d`

## Listing sessions

To list all sessions, use `tmux ls` command

## Attaching

To attach to a session, use `tmux a -t <session_name>`

## New window

To create a new window, use `CtrlB + c`

## Copy Mode

To enter copy mode, use `CtrlB + [`

## Top of Copy Mode

To go to the top of the screen in copy mode, use `CtrlB + g`

## Bottom of Copy Mode

To go to the bottom of the screen in copy mode, use `CtrlB + G`

## Exit Copy Mode

To exit copy mode, use `q`

## Split Vertically

To split windows vertically, use `CtrlB + %`

## Split Horizontally

To split windows horizontally, use `CtrlB + "`

## Moving Panes

To move between windows, use `CtrlB + <arrow_key>`

## Resizing Panes

To resize windows, hold `CtrlB` and use arrow keys

## Move between windows

To move between different windows, use `CtrlB + <number>`

## Kill Windows

To kill an unresponsive window, use `CtrlB + k` 

## Closing Session

To close a session, use `exit`

## New Named Session

To create a new session with a name, use `tmux new -s <name>`