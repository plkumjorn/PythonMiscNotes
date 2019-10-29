# Essential Screen
**Screen** is a terminal multiplexer allowing you to start a screen session which continues to run any process you order even when the window is not visible or you get disconnected.

## Start a screen
		screen -L -S <session_name>

- -L means that everything printed to the terminal screen will be logged and stored in `screenlog.0` at the location where the screen command was called.
- -S `<session_name>` allows you to name the screen session

## Detach / List / Reattach
1. Detach from a screen session

		Ctrl+a +d
2. List all the active screen session

		screen -ls
		>> There is a screen on:
        >> 		31327.SNLI_full_training        (29/10/19 21:40:00)     (Detached)
		>> 1 Socket in /run/screen/S-pl1515.
3. Reattach to a screen

		screen -r <screen_id>

## Multiple windows in a screen session

See [here](https://linuxize.com/post/how-to-use-linux-screen/#working-with-linux-screen-windows)