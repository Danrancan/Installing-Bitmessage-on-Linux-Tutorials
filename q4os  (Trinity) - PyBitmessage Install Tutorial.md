## Properly Installing PyBitmessage on q40s (Trinity) "The Long Way"

### STEP 1: (The Long Way)

###### Install all necessary PyBitmessage dependancies, as well as apt-file (for the sudo apt-file search command, incase you need to find some extra packages) by copying and pasting the below command into your terminal...

`sudo apt update && sudo apt upgrade && sudo apt install -y apt-file && sudo apt-file update && sudo apt-get install -y python-pyopencl python-msgpack python-setuptools python-qt4 git libssl-dev libcap-dev python-prctl build-essential --reinstall`

### STEP 2: (The Long Way)
`git clone https://github.com/Bitmessage/PyBitmessage.git $HOME/PyBitmessage`

### STEP 3 (The Long Way)
###### Move into your cloned PyBitmessage directory, and verify that you have all the required dependencies.
`cd $HOME/PyBitmessage/ && python checkdeps.py`
###### If you see the message "cc1plus: warning: command line option ‘ -Wstrict-prototypes’ is valid for C/ObjC but not for C++" then ignore it.
###### If you see any missing dependancies other than the above two issues, search for and download them with `sudo apt-file search <missing-dependancy>`

### Step 4 (The Long Way)
###### Install bitmessage as a user so you dont need, and it doesn't use root permissions. It is more secure this way.
`python setup.py install --user`

### Step 5 (The Long Way)
###### Add the PyBitmessage directory to your $PATH and source ~/.profile
`export PATH="${PATH:+${PATH}:}~/.local/bin" && source ~/.profile`

### Step 6 (The Long Way)
###### Create a bash script that starts PyBitmessage with the command "bitmessage" automatically and checks for updates before load time
`echo '#!/bin/bash' | cat >> $HOME/.local/bin/bitmessage && echo "# This is an automatically generated script to update and start bitmessage when you type the word "bitmessage" on the command line" | cat >> $HOME/.local/bin/bitmessage && echo "export TMPHOME=$PWD" | cat >> $HOME/.local/bin/bitmessage && echo "cd $HOME/PyBitmessage/ && git pull" | cat >> $HOME/.local/bin/bitmessage && echo "cd $TMPHOME" | cat >> $HOME/.local/bin/bitmessage && echo "$HOME/.local/bin/pybitmessage" | cat >> $HOME/.local/bin/bitmessage`
