# motd-files

This repository serves as a container for all of my motd files I use. 

## What is a 'motd'?
When you login to a system (e.g. via ssh), your system will prompt you with the **m**essage **o**f **t**he **d**ay (motd). Normally the text to be shown there is stored under `/etc/motd` but there was demand for dynamic `motd`s. That's when the package `update-motd` became popular. The history of that is kinda weird and crazy, that's why you find a lot of confusing articles out there on how to set it up (which might be way outdated by now).

## How to use it?
Setting up a dynamic motd is quite easy on a modern debian or ubuntu os. My reference is [this great article](https://ownyourbits.com/2017/04/05/customize-your-motd-login-message-in-debian-and-ubuntu/) written by @nachoparker.

If you have an up to date debian or ubuntu you can start right away.
```cd /etc/update-motd.d/```
After opening that directory you can download/create your own motd script files there. One important thing: the scripts inside that folder will be executed in the order of their names (alphabetically) ascending. That means a script called "bar" will be executed before a script called "foo". That's why most of the scripts in that folder will have special names beginning with a double digit number such as "10-foo" and "20-bar" (that way you can have foo before bar).

Make sure you are root when you want to store files into that directory! Downloading the files is easy. Just open a GitHub repo, choose a script you want to download, click on "Raw" on the upper right side of the file and copy its link.
Since we are inside the correct directory, we don't need to specify the `-O` parameter.
```wget https://raw.githubusercontent.com/d-Rickyy-b/motd-files/master/10-header```

One of the most important steps is to make the files executable!
```chmod a+x 10-header```

Now we are nearly finished. Go ahead and delete your current `/etc/motd` file with
```rm /etc/motd```

If you now login to your system via ssh it should work just fine. If it does not, you might need to check your `/etc/ssh/sshd_config` server config. You must use PAM for this to work `UsePAM yes`.
Also you need to check if your `/etc/pam.d/sshd` config file contains the following content:

```
# Print the message of the day upon successful login.
# This includes a dynamically generated part from /run/motd.dynamic
# and a static (admin-editable) part from /etc/motd.
session    optional     pam_motd.so  motd=/run/motd.dynamic
session    optional     pam_motd.so noupdate
```

## Demo of the motd files
Here is a screenshot of the motd one of my servers

![Screenshot](https://raw.githubusercontent.com/d-Rickyy-b/motd-files/master/demo.png)

If you have any questions, don't hesitate to contact me.