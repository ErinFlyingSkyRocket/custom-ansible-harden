This repository contains a customized version of the Konstruktoid Ubuntu Hardening Ansible role.

Source codes referenced from konstruktoid: 

Ansible Role for Server Hardening:

https://github.com/konstruktoid/ansible-role-hardening

https://galaxy.ansible.com/ui/standalone/roles/konstruktoid/hardening

## Summary of Modified Commented Out Code

**Disabled UFW**: UFW was disabled as we had switched to use nftables instead due to its flexibility and efficiency with more advanced features, performance and more scalable. 

**Switched to Chrony**: We disabled timesyncd in favor of Chrony for time synchronization, which offers better stability and flexibility.

**Service Optimization**: Unused services like vsftpd, rsync, and apache2 were initially disabled for security reasons, though apache2 was later manually installed to support the web server functionality.

## The rest of the hardening measures implemented by Konstruktoid in the untouched areas remain robust for securing the server. These include:

**SSH Configuration Hardening**: Disabling root login and enforcing key-based authentication strengthens access control.

**Audit Logs and File Integrity**: Construction of robust logging configurations and ensuring file integrity checks are in place.

**Package Management**: Ensuring only necessary packages are installed, reducing attack vectors by minimizing the software footprint.

**Sysctl Hardening**: Kernel parameters were optimized to secure networking and prevent IP forwarding, spoofing, and other potential threats.

**Security Updates**: Regular updates were enforced for all installed packages to patch known vulnerabilities.

**SUID Blocklist**: We blocked unused commands with the SUID/SGID permissions to limit potential privilege escalation risks. This ensures that only the necessary binaries retain these elevated privileges.

**Disable IPv6**: Since IPv6 was not in use for our environment, we disabled it entirely to reduce attack surfaces that could be exploited if left enabled.

**Encryption**: We enforced encryption for data transmissions, ensuring secure communication between services, further minimizing risks from eavesdropping or data tampering.

**Password Enforcement**: Password strength was strictly enforced by utilizing strong password policies that require complex inputs. We also adjusted the default MOTD (Message of the Day) to inform users of the login policies and security expectations.

**User Umask Adjustments**: We configured the user umask to ensure that newly created files and directories have stricter default permissions, which helps prevent unauthorized access.

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
#### a) Check if firewall is configure
"bash isFirewall.bash"
#### b) Install nftables
"apt install nftables"
#### c) Disabled ufw if exist (Skip if doesn't exist)
"apt purge ufw"
#### d) Ensure no iptables rules exist (Skip if doesn't exist)
"iptables -L"
"ip6tables -L"
#### e) Flush iptables if rules exist (Skip if it's empty)
"iptables -F"
"ip6tables -F"
#### f) Save the script for nftables as /etc/nftables.rules
  ##### Run the following command to load the file into nftables
  "nft -f /etc/nftables.rules"
  ##### Make these rules permanent
  "nft list ruleset | sudo tee /etc/nftables.rules > /dev/null" 
  ##### Add following line to /etc/nftables.conf
  "include "/etc/nftables.rules"" 
#### g) Ensure nftables is enabled from boot
"systemctl enable nftables"
#### h) 4.3.4 to 4.3.10 is verification of nftables

