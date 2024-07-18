# Example Setup for Using this Role

Your working directory should have this structure:

roles/cisco-sg300(this project)
host_vars/switch1.yml
inventory.yml
ansible.cfg

You can get this structure by doing the following

```
mdkir roles && cd roles
git clone <this project>
cd ../
cp roles/cisco-sg300/files/example-setup/* .
```

### ansible.cfg

This just tells ansible that your inventory file is at `./inventory.yml`

### inventory.yml

Defines host names, default ports, ip addresses, and maybe some additional defaults.

### host_vars/switch1.yml

holds username and credential information for the ssh connection. Leave this out of source control for sure. If you rename your host name to something besides switch1, make sure to rename this file name too.

## Additional Requirements

### Credentials

Other than the username and the become password, this setup assumes that you have your ssh-agent configured to be able to connect to the switch. That means that you have run `ssh-add /path/to/your/ssh/key` before running any playbooks.

### Outdated KEX and other things
It did not seem to be possible to customize key exchange algorithms and stuff on the ansible side, so that means it needs to be done on the SSH side instead. You need to put this in your ~/.ssh/config file:

```
Host <IP Address>
  KexAlgorithms diffie-hellman-group1-sha1,diffie-hellman-group-exchange-sha1
  MACs hmac-sha1
  HostKeyAlgorithms ssh-rsa
  PubkeyAcceptedKeyTypes ssh-rsa
```

