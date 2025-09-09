# SSH
If you’re running your server on a mini PC, setting up SSH is optional but super convenient—it lets you access the machine from any other device on your local network without needing to sit in front of it. On the other hand, if you’re using a VM, SSH is pretty much the default way to connect, so you’ll likely already have it in place.

Here's how I set it up on my machine following a guide [^1] from DigitalOcean.

1. Update package repositories
```sh
sudo apt update
```

2. Install OpenSSH server
```sh
sudo apt-get install openssh-server
```

3. Start the SSH server (if not already started)
```sh
sudo systemctl start ssh
```

4. Verify that the computer is listening on the standard SSH ports (22)
```sh
sudo ss -ltup | grep 22
```

5. Allow connections to the SSH TCP ports if using UFW
```sh
sudo ufw allow OpenSSH
# or
sudo ufw allow ssh
```

6. Connect to the SSH server
```sh
ssh <user>@<ip>
```

7. Create a private / public key pair on the client (passphrase is optional but recommended)
```sh
ssh-keygen -t ed25519
```

8. Secure copy the public key to the server
```sh
scp <key>.pub <user>@<ip>:~/.ssh/<key>.pub
```

10. Add the public key to the `authorized_keys` file of the server

11. You can also do steps 9 & 10 with one command
```sh
ssh-copy-id -t <path-to-key> <user>@<ip>
```

[^1]: [SSH Essentials: Working with SSH Servers, Clients, and Keys](https://www.digitalocean.com/community/tutorials/ssh-essentials-working-with-ssh-servers-clients-and-keys)