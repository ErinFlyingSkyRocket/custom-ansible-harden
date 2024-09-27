Source codes referenced from konstruktoid: 

Ansible Role for Server Hardening:

https://github.com/konstruktoid/ansible-role-hardening

https://galaxy.ansible.com/ui/standalone/roles/konstruktoid/hardening


## Guide to running the Ansible script:

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

##### Change the IP address of the line to the instance target
"sudo nano inventory"

__________________________________________

### Step 4: Running the script
##### Run the harden.yml with sudo to ensure it has permission to run all tasks
"sudo ansible-playbook -i inventory harden.yml"
__________________________________________
### Step 5: nftables Firewall implementation
a) Check if firewall is configure
"bash isFirewall.bash"
b) Install nftables
"apt install nftables"
c) Disabled ufw if exist (Skip if doesn't exist)
"apt purge ufw"
d) Ensure no iptables rules exist (Skip if doesn't exist)
"iptables -L"
"ip6tables -L"
e) Flush iptables if rules exist (Skip if it's empty)
"iptables -F"
"ip6tables -F"
f) Save the script for nftables as /etc/nftables.rules
  ### Run the following command to load the file into nftables
  "nft -f /etc/nftables.rules"
  ### Make these rules permanent
  "nft list ruleset | sudo tee /etc/nftables.rules > /dev/null" 
  ### Add following line to /etc/nftables.conf
  "include "/etc/nftables.rules"" 
g) Ensure nftables is enabled from boot
"systemctl enable nftables"
h) 4.3.4 to 4.3.10 is verification of nftables

