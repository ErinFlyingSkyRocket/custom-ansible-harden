Guide to running the Ansible script:

Step 1: Do the appropriate updates and ensure ansible is installed in the environment to run the script
Run the 3 following commands
sudo apt update
sudo apt install ansible -y

Step 2: Download the git repository with the following commands
sudo apt install git -y
git clone https://github.com/ErinFlyingSkyRocket/custom-ansible-harden.git

Step 3: Insert your SSH key to the
# Change directory into the downloaded folder and make the required changes.
cd ~/custom-ansible-harden

nano .ssh/testlab.pem
sudo chmod 400 .ssh/testlab.pem


![image](https://github.com/user-attachments/assets/bd3213db-7576-4fa5-9516-b58245cb29db)
