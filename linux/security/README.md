# Configure linux server security

Following are the steps to configure linux server security.

## Update your software

Get automatic security updates for your server.

```bash
sudo apt update
sudo apt install unattended-upgrades
sudo dpkg-reconfigure --priority=low unattended-upgrades
```

## Don't forget docker containers

All docker containers should be updated regularly. The best way is to destroy and recreate them.

We can use some service like watchtower to update docker containers automatically.

## Secure your SSH access

### Create a new user for SSH access

1. Create a new user

```bash
sudo useradd <username> -m -s /bin/bash -c "<comment>"
```

2. Add the user to the sudo group. (Additionally we can add the user to other groups. For e.g here we are adding the user to the docker and adm groups)

```bash
sudo usermod -aG sudo,adm,docker <username>
```

3. Create password for the user

```bash
sudo passwd <username>
```

### Create a new SSH key for the user on your local machine

1. Generate a new SSH key

```bash
ssh-keygen -b 4096 -C "<comment>"
```

> It's a good practice to use a passphrase for your SSH key.

2. Copy the public key to the server

i. Create a directory named .ssh in the user's home directory

```bash
sudo mkdir /home/<username>/.ssh
```

ii. Copy the public key to the server

On your client machine

```bash
scp ~/.ssh/id_rsa.pub <username>@<server-ip>:/home/<username>/.ssh/authorized_keys
```

iii. Change the permissions of the authorized_keys file

```bash
sudo chown -R <username>:<username> .ssh
```

### Disable root login

1. Open the sshd_config file

```bash
sudo vim /etc/ssh/sshd_config
```

2. Change the following lines

```bash
PermitRootLogin no
PasswordAuthentication no
```

3. Restart the ssh service

```bash
sudo systemctl restart ssh
```

## Don't expose unused services

### Overview of services

Get a list of all the services running on your server

```bash
sudo ss -ltpn
```

## Use a firewall

### Allow only required ports

This will allow only the ports 22, 80 and 443.

**Note:** _Make sure that you are not locked out. So allow ssh port first._

```bash
sudo ufw allow 22
sudo ufw allow 80
sudo ufw allow 443
```

### Enable the firewall

> **Note:** _For ports exposed by docker containers, ufw will not work. We need to use iptables to allow those ports. We can also use reverse proxy to expose the ports._

```bash
sudo ufw enable
```

## Use a reverse proxy

Using some reverse proxy like nginx or traefik we can expose the ports of docker containers when possible.

## Use a IPS (Intrusion Prevention System)

This will help us to detect and block malicious traffic.

### Install fail2ban

Goes through the log files and blocks the IP addresses that are trying to access the server with invalid credentials.

1. Install fail2ban

```bash
sudo apt install fail2ban
```

2. Enable the service

```bash
sudo systemctl enable fail2ban --now
```

3. Check the status of the service

```bash
sudo systemctl status fail2ban
```

4. Get the logs

```bash
sudo fail2ban-client status
```

5. You can also get specific logs for a jail like sshd.

```bash
sudo fail2ban-client status sshd
```

## Isolate your application

Isoalate your application from the rest of the system using docker containers or apparmor.
