# Properly Installing Bitmessage on Debian 10 KDE
##### A tutorial provided by [Nerd-Tech.net](https://www.nerd-tech.net) 

This tutorial will help you properly install [PyBitmessage](https://github.com/Bitmessage/PyBitmessage) with all dependencies on a cleanly installed Debian 10 KDE distribution. It requires the use of your terminal application. First read the instructions for each step, then copy and paste each command below the instructions into your terminal and press enter.

#### 1-7 "The Long Way" 
#### (Skip to step 8-10 for "The Short Way")

## Step 1

Install all necessary [PyBitmessage](https://github.com/Bitmessage/PyBitmessage) dependancies, as well as [apt-file](https://packages.debian.org/buster/apt-file) (for the ```sudo apt-file search``` command), incase you need to find some extra packages.

```markdown
sudo apt update && sudo apt install -y apt-file && sudo apt-file update && sudo apt install -y python python-pip/stable python-msgpack python-qt4 python-pyopencl python-setuptools python-prctl openssl libssl-dev git libcap-dev libcanberra-gtk-module/stable python-notify python-notify2 libmessaging-menu-dev build-essential --reinstall
```
## Step 2
Clone the Official Bitmessage Repo to your home directory (or whatever directory you want to store your bitmessage repo in).
```
git clone https://github.com/Bitmessage/PyBitmessage $HOME/PyBitmessage
```
## Step 3
Move into your cloned PyBitmessage directory, and verify that you have all the required dependencies.
```
cd $HOME/PyBitmessage/ && python checkdeps.py
```
If you see the message _"***cc1plus***: ***warning***: command line option ‘ ***-Wstrict-prototypes***’ is valid for C/ObjC but not for C++"_
then ignore it.

If you see the message _"Optional dependency \`pip install .[prctl]\` would require \`apt-get install libcap-dev python-prctl\` to be run as root"_
then ignore it.

If you see any missing dependancies other than the above two issues, search for and download them with ```sudo apt-file search missing-dependancy``` or with ```sudo apt file search missing-dependency```

## Step 3
Install bitmessage as a user so you dont need, and it doesn't use root permissions. It is more secure this way.
```
setup.py install --user
```
## Step 4
Add the PyBitmessage directory to your $PATH and source ~/.profile
```
export PATH="${PATH:+${PATH}:}~/.local/bin" && source ~/.profile
```
## Step 5
Create a bash script that starts PyBitmessage with the command "bitmessage" automatically and checks for updates before load time 
```
echo '#!/bin/bash' | cat >> $HOME/.local/bin/bitmessage && echo "# This is an automatically generated script to update and start bitmessage when you type the word "bitmessage" on the command line" | cat >> $HOME/.local/bin/bitmessage && echo "export TMPHOME=$PWD" | cat >> $HOME/.local/bin/bitmessage && echo "cd $HOME/PyBitmessage/ && git pull" | cat >> $HOME/.local/bin/bitmessage && echo "cd $TMPHOME" | cat >> $HOME/.local/bin/bitmessage && echo "$HOME/.local/bin/pybitmessage" | cat >> $HOME/.local/bin/bitmessage
```
## Step 6
Give your newly created bash script execute permissions
```
chmod a+x $HOME/.local/bin/bitmessage
```
## Step 7
Start bitmessage and enjoy!
```
bitmessage
```
## Done!

##### "The Short Way"
# Installing Bitmessage and all dependencies on a Debian 10 KDE clean install
# Copy and paste the uncommented (indicated by a line that doesnt start with #) commands into your terminal.

## Step 8)
Below is a one-liner to:
Go to your home folder home folder
Install apt-file (incase you need to find some extra packages)
Install your dependancies 
Clone the official PyBitmessage repository
Move into the PyBitmessage cloned directory
Check if you still have any missing dependancies.
```
cd $HOME && sudo apt update && sudo apt install -y apt-file && sudo apt-file update && sudo apt install -y python python-pip/stable python-msgpack python-qt4 python-pyopencl python-setuptools python-prctl openssl libssl-dev git libcap-dev libcanberra-gtk-module/stable python-notify python-notify2 libmessaging-menu-dev build-essential --reinstall && git clone https://github.com/Bitmessage/PyBitmessage $HOME/PyBitmessage && cd ~/PyBitmessage && python $HOME/PyBitmessage/checkdeps.py
```
## Step 9) 
Below is a one-liner to:
Install bitmessage as a user
Add the PyBitmessage directory to your $PATH 
Create a simple bash script that updates PyBitmessage & starts PyBitmessage everytime you open it.
Name the generated bitmessage script to "_bitmessage_", 
Make the generated bitmessage script executable (chmod a+x) 
Add the installed PyBitmessage binary directory ($HOME/.local/bin} to your $PATH. 

```
python $HOME/PyBitmessage/setup.py install --user && export PATH="${PATH:+${PATH}:}~/.local/bin" && source ~/.profile && echo '#!/bin/bash' | cat >> $HOME/.local/bin/bitmessage && echo "# This is an automatically generated script to update and start bitmessage when you type the word "bitmessage" on the command line" | cat >> $HOME/.local/bin/bitmessage && echo "export TMPHOME=$PWD" | cat >> $HOME/.local/bin/bitmessage && echo "cd $HOME/PyBitmessage/ && git pull" | cat >> $HOME/.local/bin/bitmessage && echo "cd $TMPHOME" | cat >> $HOME/.local/bin/bitmessage && echo "$HOME/.local/bin/PyBitmessage" | cat >> $HOME/.local/bin/bitmessage && chmod a+x $HOME/.local/bin/bitmessage
```
## Step 10)
Activate bitmessage 
```
bitmessage
```
## Final Step
Bitmessage should start up and run.
Check that the only warnings you get are the ones listed below.
Contact developers if you want to play around with namecoin. I know nothing about it.
```
2020-12-13 10:40:05,136 - WARNING - Using default logger configuration
2020-12-13 10:40:05,545 - WARNING - /home/boo/.namecoin/namecoin.conf unreadable or missing, Namecoin support deactivated
2020-12-13 10:40:05,546 - WARNING - There was a problem testing for a Namecoin daemon. Hiding the Fetch Namecoin ID button
```
If you get other warnings. Find the missing dependencies.

## All done.

