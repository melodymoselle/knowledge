# Ubuntu 16.04

1. Add SSH key on server creation
2. Login into server with *root* user
	- `$ ssh root@your_server_ip`
	- Accept warning about host authenticity on first login
3. Create new user
	- `$ adduser newuser`
4. Add new user to *sudo* user group
	- `$ usermod -aG sudo newuser`
5. Add public SSH key to new user
	- Copy SSH key from local machine
		- `$ cat ~/.ssh/id_rsa.pub`
	- On server, temporarily switch to new user
		- `$ su - newuser`
	- Create new SSH directory
		- `$ mkdir ~/.ssh`
	- Restrict permissions to new directory
		- `$ chmod 700 ~/.ssh`
	- Create and open new file 'authorized_keys' in .ssh directory
		- `$ nano ~/.ssh/authorized_keys`
	- Paste public SSH key from clipboard
	- Close and save file
	- Restrict permissions to new file
		- `$ chmod 600 ~/.ssh/authorized_keys`
	- Exit from temp user
		- `$ exit`
6. Log out from *root* and login as *newuser*
7. Change settings in SSH configuration
	- Open file
		- `$ sudo nano /etc/ssh/sshd.config`
	- Uncomment the following settings, edit if needed
		```
		PasswordAuthentication no
		PubkeyAuthentication yes
		ChallengeResponseAuthentication no
		PermitRootLogin no
		```
	- Close and save file
	- Reload SSH daemon
		- `$ sudo systemctl reload sshd`