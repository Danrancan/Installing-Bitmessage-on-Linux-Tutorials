Properly Installing PyBitmessage on q40s (Trinity)
"The Long Way"


###STEP 1: (The Long Way)
#Install all necessary PyBitmessage dependancies, as well as apt-file (for the sudo apt-file search command, incase you need to find some extra packages) by #copying and pasting the below command into your terminal...
sudo apt update && sudo apt upgrade && sudo apt install -y apt-file && sudo apt-file update && sudo apt-get install -y python-pyopencl python-msgpack python-setuptools python-qt4

###STEP 2: (The Long Way)
git clone https://github.com/Bitmessage/PyBitmessage.git $HOME/PyBitmessage

Step 3 (The Long Way)
