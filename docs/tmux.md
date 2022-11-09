# Splitting screen in terminal
The purpose of splitting terminal screen is to see on one terminal window two panes with skycharge-cli monitor and skycharge-cli show-dev-params at the same time for demo.
![tmux-screen-split](assets/tmux.png)

## Installing tmux
The tmux is installed and avaliable by default on skycharge BB. In case the package is not missing install it with:
```shell
sudo apt-get update
sudo apt-get install tmux
```

## Using tmux
Creat a new session (window):
```shell
tmux new -s [session_name]
```
Exit session:
```shell
exit
```
List existingrunning sessions:
```shell
tmux ls
```
Connecting to a running session
```shell
tmux attach -t 0
```


### Pane Handling
By default, the prefix is CTRL+B followed by a command.
To check the current prefix shortcut run:
```shell
tmux show-options -g | grep prefix
```

- Split panes vertically	<kbd>Ctrl</kbd> + <kbd>B</kbd> + <kbd>%</kbd>
- Split panes horizontally    <kbd>Ctrl</kbd> + <kbd>B</kbd> + <kbd>"</kbd>
- Toggle last active plane	<kbd>Ctrl</kbd> + <kbd>B</kbd> + <kbd>;</kbd>
- Swap panes	<kbd>Ctrl</kbd> + <kbd>B</kbd> + <kbd>o</kbd>
- Kill pane	<kbd>Ctrl</kbd> + <kbd>B</kbd> + <kbd>x</kbd>
- Show pane numbers	<kbd>Ctrl</kbd> + <kbd>B</kbd> + <kbd>q</kbd>
- Move plan left	<kbd>Ctrl</kbd> + <kbd>B</kbd> + <kbd>{</kbd>
- Move plan right	<kbd>Ctrl</kbd> + <kbd>B</kbd> + <kbd>}</kbd>
- Switching between panes	<kbd>Ctrl</kbd> + <kbd>B</kbd> + <kbd>arrow key</kbd>


To open a new session called Skycharge run:
```shell
tmux new -s Skycharge
```
split it horizontaly: <kbd>Ctrl</kbd> + <kbd>B</kbd> + <kbd>%</kbd>\
move between panes: <kbd>Ctrl</kbd> + <kbd>B</kbd> + <kbd>arrow key</kbd>

### Script automation
The screen split and running skkycharge-cli commands can be automated with scrip below.
To add the script create an empty file i.e split_script.sh
```bash
touch split_script.sh
```
edit the script file with:
```bash
nano split_script.sh
```

copy & paste the script below into the script file, save and exit

```bash
#!/bin/sh
tmux new -d -s Skycharge
tmux send -t Skycharge "skycharge-cli monitor" ENTER
tmux split-window -v
tmux send -t Skycharge.1 "skycharge-cli show-dev-params" ENTER
tmux attach -t Skycharge
```
make the script exetuable:
```bash
chmod +x split_script.sh
```

and run it with:
```bash
./split_script.sh
```

To exit and close the tmux panes run:

<kbd>Ctrl</kbd> + <kbd>B</kbd> + <kbd>x</kbd>\
<kbd>Ctrl</kbd> + <kbd>B</kbd> + <kbd>x</kbd>
