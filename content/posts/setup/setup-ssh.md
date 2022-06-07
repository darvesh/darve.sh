---
# author: "Me"
title: "Setup SSH"
date: "2022-05-18"
description: ""
tags: ["ssh","config"]
aliases: ["SSH"]
ShowToc: false
TocOpen: true
---

## Generate key
{{< highlight bash "linenos=false" >}}
ssh-keygen -t ed25519
{{< /highlight >}}


## Write config
Create a file named `config` inside `~/.ssh` and add the following.
{{< highlight bash "linenos=false" >}}
Host <server-name>
 Hostname <ip>
 User <username>
 IdentityFile <path-to-private-key>
{{< /highlight >}}

Now you can log in to your server easily with
`ssh <server-name>` instead of having to type `ssh -i <path-to-private-key> <username>@<Hostname>`

## Fix disconnection on idle
Client will keep sending null packets every 100 seconds to keep the connection alive. Add 
{{< highlight bash "linenos=false" >}}
ServerAliveInterval 100
{{< /highlight >}}

to either 
```bash
sudo vi /etc/ssh/ssh_config
```
or
```bash
vi ~/.ssh/config
```
Alternatively, you can do `ssh -o ServerAliveInterval=100 me@remote`

## Reverse Port Forwading
Add these lines to `/etc/ssh/sshd_config` on your server
```bash
GatewayPorts clientspecified
AllowTcpForwarding yes
```
Then open the terminal on your local computer, paste the following and change the values suitably
```bash
ssh -o ExitOnForwardFailure=yes -v -N -R "*:$SERVER_PORT:*:$CLIENT_PORT" server_name
```

Flags:\
`R` = Specifies that connections to the given TCP port or Unix socket on the remote (server) host are to be forwarded to the local side.\
`N`	= Do not execute a remote command, in simple words, do not log in to the server.\
`v` = Verbose mode.  Causes ssh to print debugging messages about its progress.

`server_name` is either `username@ip` or server name that you configured on your `~/.ssh/config`\
If you want to bind to only IPv4 addresses, use `0.0.0.0` instead of `*`

If there is frequent disconnection, follow [this](#fix-disconnection-on-idle) to fix it.