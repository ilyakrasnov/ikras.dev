---
layout: post
title:  "SSH config on Mac"
date:   2019-10-30 09:31:56 +0300
img: switches.jpg
tags: mac
credit: Jordan Harrison 

---

Setting up `ssh` on a Mac is pretty easy. All you need to do is 

### Edit the `~/.ssh/config` file like this

```

Host *
    UseKeychain yes
Host host1
    HostName SOME_IP_ADDRESS
    IdentityFile ~/.ssh/YOUR_KEY_FILE.pem
    User username
Host host2
    HostName SOME_OTHER_IP_ADDRESS
    IdentityFile ~/.ssh/YOUR_KEY_FILE_2.pem
    User username

```

For each host add following information: 

* hostname its just an alias for your future use
* ip address
* path to your key file (store them in the `~/.ssh/` folder)
* username

### Connect to your hosts

Typing `ssh host1` in the terminal will now connect you to the given host.


### (Optional - Convert `.ppk` to `.pem`)

If you happen to have a `.ppk` key file (from a windows machine) you need to convert it to `.pem`

Navigate to the folder where you store the key files and run:

```puttygen YOUR_KEY_FILE.ppk -O private-openssh -o YOUR_KEY_FILE.pem```
