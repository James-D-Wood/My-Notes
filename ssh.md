# ssh - my cheat sheet

## authentication
Note: On the remote server, the public key must be copied to a file within the user’s home directory at ~/.ssh/authorized_keys

Auth Steps
1. Client tries to connect, specifies with which public key.
2. Server encrypts a random message with public key and sends it back to the client.
3. Client decrypts with private key, hashes the message, and sends it back.
4. Server verifies.


## security techniques
- use SSH keys over passwords -> asymmetrical encription is much safer
- disable password auth
- change port from default
- limit users 
- limit connections (prevent brute force)
- turn off graphical windows (x11 forwarding)
- turn off tcp port forwarding
- use tcp filters (whitelist home address / blacklist all)
- set idle timeout (ClientAliveInterval)
- disable empty passwords (PermitEmptyPasswords)
- limit MaxAuthTries
- set up email notification of login
- custom banner! :)


## useful commands

Control whether server is running (not that stopping the server does not complete until all connections have exited)

`$ sudo systemctl [start/restart/stop] ssh`

Check if the server is running

`$ ps -A | grep sshd`

Check if it is listening and on what ports

`$ sudo ss -lnp | grep sshd`

Check for connection logs

`$ cat /var/log/auth.log | grep 'onnect'` 

SCP Format

`$ scp [OPTION] [user@]SRC_HOST:]file1 [user@]DEST_HOST:]file2`

Important files:
```sh
# tcp wrappers
/etc/hosts.allow
/etc/hosts.deny

# ssh server config
/etc/ssh/sshd_config
```


## definitions

SSH daemon - software listens for connections on a specific network port, authenticates connection requests, and spawns the appropriate environment if the user provides the correct credentials

## sources

- https://infosec.mozilla.org/guidelines/openssh
- https://www.digitalocean.com/community/tutorials/ssh-essentials-working-with-ssh-servers-clients-and-keys
- https://securitytrails.com/blog/mitigating-ssh-based-attacks-top-15-best-security-practices
- https://help.ubuntu.com/community/SSH/OpenSSH/Configuring
