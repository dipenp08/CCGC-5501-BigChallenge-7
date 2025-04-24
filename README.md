Challenge: Bastion Host

A Bastion Host is a hardened server for security reasons to allow for controlled entry into a private network. Bastion hosts are often used by attackers as an entry point into the inner systems. Your mission in this exercise is to identify misconfigurations, weak passwords, or open services that can lead to unauthorized access.

How to Solve the Challenge

1. Find the Bastion Host
•	Look for public IP addresses in the setup.
•	Scan for open ports and services using nmap:
nmap -sV -p- <target-IP>  
•	Watch for services like: SSH (Port 22), RDP (Port 3389). 
2. Check SSH Access
•	If SSH is open, test for weak or default passwords:
hydra -L users.txt -P passwords.txt ssh://<target-IP>  
•	If SSH keys are used, check for insecure settings in .ssh/authorized_keys.
3. Look for Privilege Escalation
•	Once inside, check what commands you can run with admin rights:
sudo -l  
•	Look for private keys stored in: /home  /etc/ssh/
•	Check for passwords saved in config files.
4. Move Deeper into the Network
•	If the bastion host has access to other systems, find internal connections:
•	ip a  
netstat -rn  
•	Use SSH proxying to access internal systems:
ssh -D 1080 user@target  

Recommendations 

•	Multi-Factor Authentication (MFA) for SSH.
•	Allow SSH access from trusted IPs.
•	Use strong passwords and regularly update them.

Final Thought

If a bastion host is not properly secured, attackers can use it to break into the network. Protect it with strict security controls and monitoring to stop unauthorized access.
