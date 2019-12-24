---
layout: post
title: Quickly connecting to a remote Jupyter server
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

I access Jupyter from my laptop computer by using SSH to forward the port that Jupyter is running on, for instance for port `8888`, I'd run something like:

```bash
ssh -N -L localhost:8888:localhost:8888 sam@myserver.samgehman.com
```

Running this command continues to forward the port until an exit key command is pressed. This works well, but I started to realize that I was often also wanting to start a shell on the remote server simultaneously. This meant that I'd have two terminal windows open, one for port forwarding and one for controling the remote terminal.

To make this easier, I found a few interesting 
