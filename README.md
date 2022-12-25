# ssh-hardening-ansible
Ansible script for ssh hardening 

```

hosts: all
become: true
vars:

Set the desired SSH port number
ssh_port: 22

tasks:

name: Ensure that the SSH service is running
service:
name: ssh
state: started

name: Ensure that the SSH service is enabled
service:
name: ssh
enabled: true

name: Ensure that the SSH port is set to the desired value
lineinfile:
path: /etc/ssh/sshd_config
regexp: '^#?Port .*'
line: "Port {{ ssh_port }}"
notify:

restart ssh
name: Ensure that password authentication is disabled
lineinfile:
path: /etc/ssh/sshd_config
regexp: '^#?PasswordAuthentication .*'
line: "PasswordAuthentication no"
notify:

restart ssh
name: Ensure that root login is disabled
lineinfile:
path: /etc/ssh/sshd_config
regexp: '^#?PermitRootLogin .*'
line: "PermitRootLogin no"
notify:

restart ssh
name: Ensure that only strong ciphers and MACs are used
lineinfile:
path: /etc/ssh/sshd_config
regexp: '^#?Ciphers .*'
line: "Ciphers chacha20-poly1305@openssh.com,aes256-gcm@openssh.com,aes128-gcm@openssh.com,aes256-ctr,aes192-ctr,aes128-ctr"
notify:

restart ssh
name: Ensure that only strong key exchange algorithms are used
lineinfile:
path: /etc/ssh/sshd_config
regexp: '^#?KexAlgorithms .*'
line: "KexAlgorithms curve25519-sha256@libssh.org,diffie-hellman-group-exchange-sha256"
notify:

restart ssh
name: Ensure that only strong MAC algorithms are used
lineinfile:
path: /etc/ssh/sshd_config
regexp: '^#?MACs .*'
line: "MACs hmac-sha2-512-etm@openssh.com,hmac-sha2-256-etm@openssh.com,hmac-ripemd160-etm@openssh.com,umac-128-etm@openssh.com,hmac-sha2-512,hmac-sha2-256,hmac-ripemd160,umac-128@openssh.com"
notify:

restart ssh
name: Ensure that only strong host key algorithms are used
lineinfile:
path: /etc/ssh/sshd_config
regexp: '^#?HostKeyAlgorithms .*'
line: "HostKeyAlgorithms ssh-ed25519-cert-v01@openssh.com,ssh-rsa-cert-

```
