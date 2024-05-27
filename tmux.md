# Tmux commands

Tmux is a terminal multiplier, we can save named sessions so we can quickly spin up what we need for a development environment or maybe application monitoring.

# Installing tmux

[Follow this](https://github.com/tmux/tmux/wiki/Installing)

### Basic commands

- open Tmux
  $ tmux
- Close tmux session
  $ exit || tmux kill-session -t <sessionName>
- Close tmux window
  $ PREFIX &

- Enter command mode
  $ PREFIX :
- List all comands:
  $ PREFIX ?

### Named sessions

We can keep things organised with named sessions
$ tmux new -s <sessionName>

### Prefix commands

Since our CLI programs run inside tmux, we need a way to tell tmux that the command we're typing is for tmux and not for the underlying application. The "CTRL -b" combination does just that. This combination is called the command prefix. You prefix each tmux command with this key combination. by pressing "CTRL -b" (that's the default) Because the prefix can be changed I will write PREFIX when the prefix keys need to be pressed for a command.
$ CTRL -b

#### Create a window that displays our CPU usage with

$ top

#### Detach from the tmux session

$ PREFIX d

#### List active tmux sessions

$ tmux list-sessions || $ tmux ls

#### Attatch to an active tmux session

If you only have 1 session running, simply using:
$ tmux attach

To attach to a specific session use:
$ tmux attach -t <sessionName>

### Create multiple windows

$ tmux new -s window -n shell
The -n flag names our window so we can easily identify it

To create a new window in a current session press:
$ PREFIX c

By default, if we don't name a window it will take the name of whateve ris runninh in it. To rename a window press:
$ PREFIX ,

### Moving between windows

To display a visual window of all windows
$ PREFIX w
To find a window
$ PREFIX f
Move to the next window:
$ PREFIX n
Move to previous window:
$ PREFIX p
$ Move to a specific window:
$ PREFIX <windowIndex>

### Using panes

$ PREFIX % (divide the window down the middle and start up a second terminal session in the new pane)
$ PREFIX " (Split the new pane in half horizontally)
To Cycle through panes press
$ PREFIX o
Or to move around you can press
$ PREFIX UP, DOWN, LEFT or RIGHT
To change the layout of the panes press
$ PREFIX spacebar
PREFIX spacebar cycles through these layours:
"even-horizontal"
"even-vertical"
"main-horizontal"
"main-vertical"
"tiled"
To break pane to a new window
$ PREFIX !

### Command mode

To enter command mode:
$ PREFIX :
From a tmux session we can open a new window that runs "top" called "processes" by running the following
$ PREFIX : new-window -n processes "top"
When we hit enter a new window will be in focus running the top process

### Configuring tmux

To configure tmux we need a .tmux.conf file in our home dir
$ touch ~/.tmux.conf
Here we can do everything from defining new key shortcuts to setting up a default environment with multiple windows, panes and running programs.
To set options in the .tmux.conf file use:
$ set-option OR $ set

Changes aren't read by tmux automatically so if you're editing your .tmux.conf file while tmux is running. You'll need to enter tmux's command mode PREFIX : and type this whenever you make a change:
$ PREFIX : source-file ~/.tmux.conf

#### Update prefixes in our .tmux.conf file

Set the default prefix from C-b to C-a
$ set -g prefix C-a
Free up the original default PREFIX (ctrl-b)
$ unbind C-b

Changing the default delay:
$ set -s escape-time 1

Update base index to 1 instead of 0:
$ set -g base-index 1

Update base pane number to 1 instead of 0
$ set -g pane-base-index 1
