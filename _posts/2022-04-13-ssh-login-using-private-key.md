---
layout: post
title: "ssh login using private key"
category: manual
---

As daily working, we always do some tedious things, like login to serveral remote servers by ssh and then type serveral times password.

we can login using private key instead of type password, just do the following easy steps:

### 1. generate ssh key in your local pc

```bash
ssh-keygen -t rsa
```

it’ll let you type the key name, leave it as default. and the next steps password also can leave it as empty.

it will generate two files:

```bash
~/.ssh/id_rsa
~/.ssh/id_rsa.pub #this one should copy to the remote server
```

### 2. copy the public key to remote server

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub remote_user@remote_server_ip
```

### 3. you can login your server just type

```bash
ssh remote_user@remote_server_ip
```

### 4. diagram

![diagram](/assets/images/2022-04-13-ssh-private-key.png)
