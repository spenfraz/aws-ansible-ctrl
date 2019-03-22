# aws-ansible-ctrl
A minimal Ansible control machine setup targeting an AWS EC2 instance. (Manually launch an EC2 instance via the AWS Console. Test the connection to the instance with the ping module.)

#### *TESTED ON* Linux Mint 19.1 Tessa Ubuntu Bionic (18.04)

### 1. Create AWS Account
---> https://aws.amazon.com/free/

### 2. Sign in
---> https://console.aws.amazon.com/

### 3. Select 'Services' then 'EC2'

### 4. Select 'Running Instances'

### 5. Click the blue 'Launch Instance' button.

### 6. Click the 'Amazon Linux 2 AMI' blue 'Select' button.

### 7. Ensure 't2.micro' is selected. Click blue 'Review and Launch' button.

### 8. Select 'Edit security groups' link. (Along right-hand side.)

### 9. Select the 'Source' dropdown box, switching from 'Custom' to 'My IP'. Click the blue 'Review and Launch' button.

### 10. Select the blue 'Launch' button.

### 11. Complete the 'Select an existing key pair or create a new key pair' modal dialogue (create a new key pair and download it to your local machine) and select the blue 'Launch' button.

### 12. After a short loading screen 'Launching Instances...' finishes, select the blue 'View Instances' button.

### 13. After the 'Instance State' is 'running' (green), copy the 'IPv4 Public IP' for the instance and replace <public-ip\> in the hosts file with it.

### 14. Move the downloaded .pem file to ~/.ssh/
        (assuming its in ~/Downloads/)
        $ mv ~/Downloads/<filename>.pem ~/.ssh/
### 15. Change permissions on .pem (only readable by root)
        $ sudo chmod 400 ~/.ssh/<filename>.pem
### 16. Replace <filename\> in the hosts file with the downloaded .pem filename.
        (hosts file so far:)
        
        [test]
        #.#.#.# ansible_ssh_private_key_file=~/.ssh/<filename>.pem ansible_ssh_user=ec2-user

### 17. Install Ansible.
        $ sudo apt install ansible
        
### 18. Append hosts file contents into /etc/ansible/hosts
        $ sudo su
        # cat hosts >> /etc/ansible/hosts
        # exit
        
### 19. Test connection with the Ansible ping module.
        'ping – Try to connect to host, verify a usable python and return pong on success'
        https://docs.ansible.com/ansible/latest/modules/ping_module.html
        
        $ ansible test -m ping
        
        (You will get the following message:)
        
        The authenticity of host '#.#.#.# (#.#.#.#)' can't be established.
        ECDSA key fingerprint is SHA256:--------------------------------------------
        ECDSA key fingerprint is MD5:--:--:--:--:--:--:--:--:--:--:--:--:--:--:--:--.
        Are you sure you want to continue connecting (yes/no)?
        
        (After typing "yes" and pressing "Enter" key.)
        
        (Success Message:)
        
        #.#.#.# | SUCCESS => {
        "changed": false, 
        "ping": "pong"
        }
