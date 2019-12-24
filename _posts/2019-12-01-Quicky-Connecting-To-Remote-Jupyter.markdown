---
layout: post
title: Quickly connecting to a remote Jupyter server with SSH
date:   2019-12-23 00:00:00 -0800
categories: productivity shell
---
# tl;dr
You can forward the port for Juptyer every time you SSH into a remote server by adding the following line to an SSH config for a specific host:
```bash
LocalForward localhost:8888 localhost:8888
```

# Motivation
I recently set up a server at my home with a GPU for training deep learning models. My current workflow is to start up a Python notebook in Jupyter, write some PyTorch model code, and train the model within the notebook. 

I access Jupyter remotely from my laptop by using SSH to forward the port that Jupyter is running on, for instance for port `8888`, I'd run something like:

```bash
ssh -N -L localhost:8888:localhost:8888 sam@myserver.samgehman.com
```

Running this command continues to forward the port until an exit key command is pressed. This works well, but I started to realize that I was often also wanting to start a shell on the remote server simultaneously.

The main problems I had with this workflow were:
1. I had to keep two terminal windows open, one for port forwarding and one for controling the remote terminal
2. It's tedious to type the port and the entire hostname of my server


# Solution
Luckily, there's a neat SSH config feature available to solve this!

My ideal solution was to forward the port for Jupyter every time I SSH'ed into my server. This can be accomplished by adding a few lines to the SSH config, located at `~/.ssh/config`.

```bash
Host myserver # a nickname for the host

  # Credentials
  HostName myserver.samgehman.com
  User sam

  # Always forward remote port 8888 as local port 8888
  LocalForward localhost:8888 localhost:8888
```

# Thanks
After I wrote this up, I realized that this approach is covered on [Leo C. Stein's blog](https://duetosymmetry.com/code/ssh-ipython-notebook-magic/). I'm planning on adding some of the features that he mentioned could be implemented, including a script to forward any port that Jupyter is launched on.
