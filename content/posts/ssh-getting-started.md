+++
title = "SSH Getting Started"
date = 2026-06-05
+++

First, install OpenSSH on both the server and the client:

```bash
sudo pacman -S openssh
```

* Enable the SSH service on both machines using the following command. Enabling `sshd` on the client is not necessary unless you want the client to accept incoming SSH connections.

```bash
sudo systemctl enable --now sshd.service
```

* Generate an SSH key pair on the client:

```bash
ssh-keygen
```

* Copy the public key to the server. You will be prompted for the password of the user account you are connecting to.

```bash
ssh-copy-id <username>@<remote_host>
```

* Connect to the server:

```bash
ssh <username>@<remote_host>
```
