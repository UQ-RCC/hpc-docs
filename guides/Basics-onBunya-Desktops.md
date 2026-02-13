# Handy Hints and Workarounds for onBunya Desktops

The onBunya desktops have been a game changer for people's access to high performance computing resources.

From time to time, users may experience minor inconvenience due to bugs or hardware malfunction.

This short note, gives some useful information for some of them.

## Desktop appears blank 

Your Desktop has become damaged and needs to be rebuilt.</br>
Close all your launched desktops and delete their associated jobs.</br>
Then, </br>
use one of 
- an ssh connection to a login node,
- the Clusters/Bunya_Shell_Access feature of onBunya,
- the Files feature of onBunya
to remove the entire Desktop folder from your home directory.

Then resubmit an onBunya desktop job and launch the desktop. 
It will take a little bit longer to launch the first time.

## 

## Expert Desktop job completes almost immediately (Invalid VGL Device)

This is generally some sort of error has occurred as the desktop environment was being set up or as you launched the desktop.

We suspect that you are hitting the "Invalid EGL device" error. Try the following.

Instead of requesting a GPU accelerated desktop from the menus, 
- request a Regular or Expert Desktop,
- add a suitable GPU using the web form,
- when the job starts, launch the desktop,
- open a terminal app in the desktop,
- load the virtualgl module using the command `module load virtualgl` in the terminal
- start your software using the command `vglrun -d egl <command>` in the terminal

- 
