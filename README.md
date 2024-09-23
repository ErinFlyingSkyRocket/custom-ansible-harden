![image](https://github.com/user-attachments/assets/9e9d5940-f21a-439f-b05f-095a612d8eb0)## Guide to running the Ansible script:

### Step 1: 

Do the appropriate updates and ensure Ansible is installed in the environment to run the script

Run the update and install Ansible:

"sudo apt update"

"sudo apt install ansible -y"

__________________________________________

### Step 2: Clone the git repository with the following commands

"sudo apt install git -y"

"git clone https://github.com/ErinFlyingSkyRocket/custom-ansible-harden.git"

__________________________________________

### Step 3: Insert your SSH key to the
##### Change the directory into the downloaded git pack (custom-ansible-harden) and make the required changes.

"cd ~/custom-ansible-harden"

##### Paste your SSH key in the .pem file and ensure permission is set to 400, else it won't run

"nano .ssh/testlab.pem"

"sudo chmod 400 .ssh/testlab.pem"

__________________________________________

### Step 4: Running the script
##### Run the harden.yml with sudo to ensure it has permission to run all tasks
"sudo ansible-playbook -i inventory harden.yml"

