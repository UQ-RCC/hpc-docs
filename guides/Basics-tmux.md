# The tmux basics

## What is tmux ?

tmux is a terminal multiplexer.
tmux enables a number of terminals to be created, accessed, and controlled from a single screen.  
tmux may be detached from a screen and continue running in the background, then later reattached.

## Why would I use tmux ?

Scenario such as you need to leave something running in an interactive session launched from a login node.

But you need to go home and that means closing your laptop.

You could handle this by
- logging into bunya
- starting a tmux terminal
- launching your interactive batch job
- starting your processing inside that interactive batch job
- detaching your session from the tmux terminal
- closing your laptop
- opening your laptop
- re-attaching to the tmux terminal session.

## Using tmux with only 5 commands/key-combinations

- create a new terminal `tmux new -s NAME`
- detach from the terminal you are in using `Ctrl-B d`
- list the terminals you have already running using `tmux list-sessions`
- re-attach to that terminal using `tmux attach -t NAME`
- terminate the terminal you are currently in using `Ctrl-B : kill-session`

## Sample Session

### Login node

```
[uquser@bunya2 ~]$ tmux new -s Test12
#launched an interactive job
#set the while loop running in the interactive job

#detached using Ctrl-B d
[detached (from session Test12)]

#What did I call that tmux session ??!!
[uquser@bunya2 ~]$ tmux list-sessions
Test12: 1 windows (created Thu Oct 31 19:39:26 2024) [207x59]

#reattach to the terminal and I get back into the interactive batch job
[uquser@bunya2 ~]$ tmux attach -t Test12

#and I see more dots than I had before

[detached (from session Test12)]
[uquser@bunya2 ~]$


```
### Compute Node

```
srun: ROUTE: split_hostlist: hl=bun048 tree_width 0
[uquser@bun048 ~]$ while [ 1 ]; do echo "."; sleep 15; done
.
.



[Test12] 0:srun*                                          "bunya2.rcc.uq.edu.au" 19:41 31-Oct-24
```


## More Info

For more info about tmux consult the manual page and online resources.
