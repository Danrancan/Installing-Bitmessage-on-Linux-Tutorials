# Properly Installing Bitmessage on Debian 10 KDE
##### A tutorial provided by [Nerd-Tech.net](https://www.nerd-tech.net) 

This tutorial will help you properly install [PyBitmessage](https://github.com/Bitmessage/PyBitmessage) with all dependencies on a cleanly installed Debian 10 KDE distribution. It requires the use of your terminal application. First read the instructions for each step, then copy and paste each command below the instructions into your terminal and press enter.

### IMPORTANT: Skip to the last step for the fast way of doing this with a single command.

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


### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.

# Installing Bitmessage and all dependencies on a Debian 10 KDE clean install
# Copy and paste the uncommented (indicated by a line that doesnt start with #) commands into your terminal.

# 1) Install your dependancies, as well as apt-file, incase you need to find some extra packagesand,
# then clone the official PyBitmessage repository, and move into that directory, then check if you still have any missing dependancies.

# Below is a single one-liner to do all of this for you. Copy & Paste it into terminal.
cd $HOME && sudo apt update && sudo apt install -y apt-file && sudo apt-file update && sudo apt install -y python python-pip/stable python-msgpack python-qt4 python-pyopencl python-setuptools python-prctl openssl libssl-dev git libcap-dev libcanberra-gtk-module/stable python-notify python-notify2 libmessaging-menu-dev --reinstall && git clone https://github.com/Bitmessage/PyBitmessage $HOME/PyBitmessage && cd $HOME/PyBitmessage/ && python $HOME/PyBitmessage/checkdeps.py

# 2) Install bitmessage as a user, add the PyBitmessage directory to your $PATH, and finally, create a simple bash script that updates & starts bitmessage everytime you open it.

# Rename the auto-generated bitmessage script to, "bitmessage", make it executable (chmod a+x), then add the installed PyBitmessage binary directory ($HOME/.local/bin} to your $PATH. 

#Below is a single one-liner to do all of this for you. Copy & Paste it into terminal.
python $HOME/PyBitmessage/setup.py install --user && export PATH="${PATH:+${PATH}:}~/.local/bin" && echo '#!/bin/bash' | cat >> $HOME/.local/bin/bitmessage && echo "# This is an automatically generated script to update and start bitmessage when you type the word "bitmessage" on the command line" | cat >> $HOME/.local/bin/bitmessage && echo "export TMPHOME=$PWD" | cat >> $HOME/.local/bin/bitmessage && echo "cd $HOME/PyBitmessage/ && git pull" | cat >> $HOME/.local/bin/bitmessage && echo "cd $TMPHOME" | cat >> $HOME/.local/bin/bitmessage && echo "$HOME/.local/bin/pybitmessage" | cat >> $HOME/.local/bin/bitmessage && chmod a+x $HOME/.local/bin/bitmessage


# PyBitmessage should be installed successfully into your user account.
# Run and activate bitmessage by typing in your terminal "bitmessage" without the quotations.
bitmessage

# Now bitmessage should be up and running. All done.

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```
