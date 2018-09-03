---
title: Linux notes
categories: it
tags: ["linux","ubuntu"]
date: 2018-09-03
---

1. Problem save file as `root` user and cannot open later: [link](https://askubuntu.com/questions/817902/unable-to-open-any-graphical-app-with-sudo/817906#817906)
2. Reinstall gksu (beed deleted by Ubuntu/Debian): [link](https://askubuntu.com/questions/1042344/i-need-an-equivalent-of-gksu-in-18-04) --> It seems that work not so well.
    ~~~
    gksu -u <user> -c <command>
    ~~~
3. Scale matlab: need to install matleb version >= R2017b
    ~~~ matlab
    s = settings;s.matlab.desktop.DisplayScaleFactor
    s.matlab.desktop.DisplayScaleFactor.PersonalValue = 2
    ~~~
4. Find in linux with command lines: [link](https://chrisjean.com/4-great-tools-to-find-files-quickly-in-ubuntu/)
5. Launching matlab without graphic ui: `matlab -nodesktop` ([link](https://blogs.mathworks.com/community/2010/02/22/launching-matlab-without-the-desktop/))
6. How to add existing user to an existing group ([link](https://askubuntu.com/questions/79565/how-to-add-existing-user-to-an-existing-group))
    ~~~
    sudo usermod -a -G groupName userName
    ~~~
7. Cannot move files to the trash/wrong owner: [link](https://askubuntu.com/questions/288513/cant-move-files-to-the-trash)
8. Check disk space with command lines: `df -h`
9. Git tip: Beautiful colored and readable output: [link](https://www.leaseweb.com/labs/2013/08/git-tip-beautiful-colored-and-readable-output/)
10. Chrome UI size & zoom levels in Ubuntu 16.04: [link](https://superuser.com/questions/1116767/chrome-ui-size-zoom-levels-in-ubuntu-16-04)
11. gnome screen shot: l[ink](https://www.howtoforge.com/tutorial/taking-screenshots-in-linux-using-gnome-screenshot/)
12. Thumbnail nautilus: go to setting, set and apply this line
    ~~~
    sudo chown -R yourusername:yourusername ~/.cache/thumbnails
    ~~~
13. Make a shortcut link to a folder/file in linux terminal: [link](https://unix.stackexchange.com/questions/226315/how-to-use-ln-s-to-create-a-command-line-shortcut)
14. Prevent bluetooth devices disconnected after sleep: [link](https://unix.stackexchange.com/questions/177998/bluetooth-mouse-disconnects)
15. Tweaks for ubuntu on surface book: [link](https://medium.com/@viettrungdang/tweaks-for-ubuntu-on-surface-book-cd05cdb8f378)
16. [linux-surface](https://github.com/jakeday/linux-surface)
17. windows shrink drive in windows: [link](https://somoit.net/windows/windows-cannot-shrink-volume-unmovable-files)
18. Shortcut to a folder in linux: [link]( https://unix.stackexchange.com/questions/226315/how-to-use-ln-s-to-create-a-command-line-shortcut)
19. **Failed to load module “canberra-gtk-module”**
    ~~~
    sudo apt install libcanberra-gtk-module libcanberra-gtk3-module
    ~~~
20. Change ownership of a folder and its children
    ~~~ bash
    # folder and its children
    chown -R thi:root folder
    # a file
    chown <user>:<group> file
    ~~~
21. *IBUS-WARNING: The owner of /home/thi/.config/ibus/bus is not root!*
22. Check the permission of curent directory: `ll <file>` or `ll`
    ![check ll](/images/posts/linux/ll-user.png)
23. Right click nautilus "Open as Administrator":
    ~~~
    sudo apt-get install nautilus-admin
    nautilus -q # restart nautilus
    ~~~
24. Cannot open matlab without sudo: change the owner permission of folder */home/thi/.matlab* to **thi*** (cf. 20)
25. Add app to dash: install **alacarte** `sudo apt-get install alacarte`
26. Turn off animation open and minimize windows on ubuntu 17.10 and later (gnome desktop): **Gnome Tweak Tools > Apperance > Animations OFF**
27. Gõ tiếng Việt SublimeText, install package `vn ime` (gõ tìm đúng như thế). Khi sử dụng thì nhấn F2.
28. Save github account as default `git config credential.helper store` then `git pull` for the first time input.



