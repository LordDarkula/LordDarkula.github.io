---
layout: post
title:  "How to setup a git server"
date:   2018-06-11
categories: programming
---

![](https://codereviewvideos.com/blog/wp-content/uploads/2015/06/git-goodness.gif)
> Source: [https://codereviewvideos.com/blog/wp-content/uploads/2015/06/git-goodness.gif](https://codereviewvideos.com/blog/wp-content/uploads/2015/06/git-goodness.gif)

Since Microsoft has acquired GitHub recently, a lot of developers are getting anxious, as 
Microsoft has a great track record of destroying it's acquisitions. If you want to stop relying on a service like GitHub 
to store your git repositories, you might want to consider creating your own git server.

## What You will need

1. *A Server* (Obviously). This can be anything ranging from a Digital Ocean Droplet
to a Raspberry Pi on your bedside table. As long as the server is running Linux you are
good to go.

2. *A Client* You need a desktop or laptop to ssh into your server. I am
using a Macbook Pro.

## Setting up SSH

SSH (Secure Shell) is a protocol that allows computers to connect securely on an unsecure
network. It is what the client will use to communicate with the server.
To connect to the server via ssh, we must know the server's local ip address.
To find it, type `ifconfig` into the terminal on the server. Find out the server's username
and password (you should have set these things when setting up the server). 

On the terminal on the client, type the following.
```bash
# replace [user] and [local_ip_address] with their appropriate values
ssh [user]@[local_ip_adress]
```
You should be asked for a password, and after entering it, you should have access to your server's
terminal. If you want to avoid having to type the ip address every time edit `/etc/hosts` file on the client
and rename the host something else.

In order to avoid having to type the password every time, you must create an ssh key.
To do that, type `ssh-keygen` into the terminal on the client side. Choose the defaults for
the following options, and the key should be placed in `~/.ssh/id_rsa`. Copy the public key over to the server
by typing the following.
```bash
cat ~/.ssh/id_rsa.pub | ssh [user]@[local_ip_adress] "mkdir -p ~/.ssh && cat >>  ~/.ssh/authorized_keys"
```
This will transfer the public key to the server and allow you to access it without typing in a password
every time. Edit `/etc/ssh/sshd_config` with vim/nano on the server and change `PasswordAuthentication yes` to `PasswordAuthentication no` 
and uncomment the line.

## Setting up git on the server
Install git onto your server with apt by typing ``sudo apt install git``.
Create a new user with `sudo adduser git`, and set the password. This user will be used
to execute all git operations. A new directory called `/home/git/` should be created on the server.
Navigate to that directory and type `sudo chown -R git:git git` to give the git user ownership
of all the files in this directory. This is where we will keep our git repositories. 

## Creating our first git repository
Create a folder called `test-repo.git` in the `/home/git` directory on the server.
Navigate to it and type `git init --bare`. This will create an empty git repository that the client can clone.
To improve security, you can change the default shell for the git user from bash to git-shell.
This will prevent users from ssh-ing into your server from the git user. To do this, find the location
of git-shell on your server by typing `which git-shell`. Type `sudo chsh git` and enter the location of the git shell.
Reboot your server for this to take effect. 

## Setting up git on the client
Create a directory called `test-repo` and add some random files to it and commit. Navigate inside of it and
type `git init` to create a git repository. Type `git remote add origin git@[local_ip_address]:/home/git/test_repo.git`.
This will link the local repository on the client to the remote repository on the server. Type `git push -u origin master`
to push.

## Adding more ssh keys
To allow more machines to login to your git server, you must ssh into the root user, and change the default login shell
for the git user back to bash. As well as that, Make sure to turn on `PasswordAuthentication` in `/etc/ssh/sshd_config` on the server. 
Now you can ssh into the git user of your server to add your new key.

## Closing Thoughts
Setting up a git repository is remarkably simple. As long as you can get ssh setup, the rest is straightforward.
However, currently you can only access your server from the same network. In order to access it from anywhere, you have
to setup something called Port Forwarding. You can learn more about it [here](https://en.wikipedia.org/wiki/Port_forwarding).
If you have any feedback, please email me at aubhrosengupta@gmail.com.

## References
https://www.youtube.com/watch?v=lXSZUuDW4nY

https://www.linux.com/learn/how-run-your-own-git-server
