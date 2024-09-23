## Guide to running the Ansible script:

Step 1: 

Do the appropriate updates and ensure Ansible is installed in the environment to run the script

Run the update and install Ansible:

"sudo apt update"

"sudo apt install ansible -y"

__________________________________________

Step 2: Download the git repository with the following commands

"sudo apt install git -y"

"git clone https://github.com/ErinFlyingSkyRocket/custom-ansible-harden.git"

__________________________________________

Step 3: Insert your SSH key to the
##### Change the directory into the downloaded folder and make the required changes.

"cd ~/custom-ansible-harden"

##### Paste your SSH key in the <<Your desired key name>>.pem file and ensure permission is set to 400, else it won't run

"nano .ssh/testlab.pem"

"sudo chmod 400 .ssh/testlab.pem"
