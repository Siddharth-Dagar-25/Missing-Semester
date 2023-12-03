Create a new directory called missing under /tmp.

Solution: We can use mkdir /tmp/missing or mkdir -p /tmp/missing.

Look up the touch program. The man program is your friend.

Solution: We can use man touch or tldr touch.

Use touch to create a new file called semester in missing.

Solution:

Run the following commands in your terminal.

cd /tmp/missing
touch semester
Or using a single comand.

touch /tmp/missing/semester
Write the following into that file, one line at a time:

#!/bin/sh
curl --head --silent https://missing.csail.mit.edu
The first line might be tricky to get working. It's helpful to know that # starts a comment in Bash, and ! has a special meaning even within double-quoted (") strings. Bash treats single-quoted strings (') differently: they will do the trick in this case. See the Bash quoting manual page for more information.

Solution:

Run the following commands in your terminal.

echo '#!/bin/sh' > semester
echo 'curl --head --silent https://missing.csail.mit.edu' >> semester
Try to execute the file, i.e. type the path to the script (./semester) into your shell and press enter. Understand why it doesn't work by consulting the output of ls (hint: look at the permission bits of the file).

Solution:

Run the following commands in your terminal.

./semester
And the terminal returns the following error.

zsh: permission denied: ./semester
Run the command by explicitly starting the sh interpreter, and giving it the file semester as the first argument, i.e. sh semester. Why does this work, while ./semester didn't?

Solution: Because the current user of the terminal does not have executable permissions to this file. However the current user has permssions to use sh command to run the file and the filename is used as an argument of sh command.

Look up the chmod program (e.g. use man chmod).

Solution: We can use man chmod or tldr chmod.

Use chmod to make it possible to run the command ./semester rather than having to type sh semester. How does your shell know that the file is supposed to be interpreted using sh? See this page on the shebang line for more information.

Solution: We can use chmod +x semester to tackle the problem.

Use | and > to write the "last modified" date output by semester into a file called last-modified.txt in your home directory.

Solution:

Run the following commands in your terminal.

./semester | grep -i last-modified | cut -d' ' -f2- > last-modified.txt
Write a command that reads out your laptop battery's power level or your desktop machine's CPU temperature from /sys. Note: if you're a macOS user, your OS doesn't have sysfs, so you can skip this exercise.

Solution:

Run the following commands to check the power level.

cat /sys/class/power_supply/BAT0/capacity
Run the following commands to check the CPU temperature.

cat /sys/class/thermal/thermal_zone0/temp