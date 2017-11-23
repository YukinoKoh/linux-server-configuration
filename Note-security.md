### Security 1. Change SSH port
Change port number in `/etc/ssh/sshd_config`
```
# What ports, IPs and protocols we listen for
Port 2200
```

### Security 2. Connect the server with SSH key
- Store the private key: /Users/[user name]/.ssh/[file name]
- `ssh [user name]@[IP address] -p [port number] -i ~/.ssh/[private key file name]`
- `ssh grader@54.249.127.217 -p 2200 -i ~/.ssh/fsndL5`
 
### Security 3. Set firewall
Set firewall UFW, ubuntu wirewall to allow only incoming connections for SSH (port 2200), HTTP (port 80), and NTP (port 123) with command line as the following, or with Amazon site Networking tab.
```
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow ssh
sudo ufw allow 2200
sudo ufw allow 80
sudo ufw allow 123
sudo ufw enable
```
Confirm the firewall status with
```
sudo ufw status
```
### Security 4. Manage packages
- `/etc/apt/sources.list`: to check installed packages
- `sudo apt-get update`: to aware of the available updates
- `sudo apt-get upgrade`: to actually upgrade the package

### Security 5. Manage user account for the server
1. Create a new user account
```
 sudo adduser [user name]
```
2. Confirm if the user added: `finger [user name]`
3. Add user permission
- Copy  `sudo cp /etc/sudoers.d/[currently permissted user] /etc/sudoers.d/[user name]`
- Reference the sudoer's file: `#includedir /etc/sudoers.d` in `/etc/sudoers`
- Add the following in [user name] file 
```
[name] ALL=(ALL) NOPASSWD:ALL
```
4. SSH key pair for the user
- Create SSH key pair locally with `ssh-keygen`
```
Enter file in which to save the key (/Users/[user]/.ssh/id_rsa): /Users/[user]/.ssh/[new SSH key name]

enter passphrase: [secret]
```
- copy and paste the public key from local to the server

Copy the key locally
```
cat ~/.ssh/[new SSH key name].pub`
```

- Paste the key at `/home/[user name]/` in the server
```
mkdir .ssh
touch .ssh/authorized_keys
```
- set access limit to the `authorized_keys` file and .ssh folder
```
chmod 700 .ssh
chmod 644 .ssh/authorized_keys
```
5. Allow the user to access server only with the private key. 
- Change `passowrdAuthentication` to `no` in `/etc/ssh/sshd_config`
- `sudo service ssh restart`: Restart server to reset the settings.

