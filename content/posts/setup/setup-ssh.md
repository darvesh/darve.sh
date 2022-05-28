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
{{< highlight bash "linenos=false" >}}
sudo vi /etc/ssh/ssh_config
{{< /highlight >}}
or
{{< highlight bash "linenos=false" >}}
vi ~/.ssh/config
{{< /highlight >}}
Alternatively, you can do `ssh -o ServerAliveInterval=100 me@remote`
