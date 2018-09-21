---
title: Linux notes
categories: it
tags: ["linux","ubuntu"]
date: 2018-09-21
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
11. gnome screen shot: [link](https://www.howtoforge.com/tutorial/taking-screenshots-in-linux-using-gnome-screenshot/)
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

	<ul class="collapsible" data-collapsible="accordion">
	<li>
	<div class="collapsible-header" markdown="1"><i class="material-icons">face</i>
	see the photo
	</div>
	<div class="collapsible-body" markdown="1">
	![check ll](/images/posts/linux/ll-user.png)
	</div>
	</li>
	</ul>

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
29. Install file `.bin`, `.run`

    ~~~ bash
    chmod +x file-name.run 
    ./file-name.run
    ~~~

30. **Matlab drive connector**: after installing, run `~/bin/MATLABConnector toggle`
31. **Install freefem++ on Ubuntu 18**
    - Install prerequired packages

        ~~~ bash
    sudo apt-get install cpp freeglut3-dev g++ gcc gfortran
    sudo apt-get install  ghostscript m4 make patch pkg-config wget python
    sudo apt install autoconf
    sudo apt-get install bison
    sudo apt-get install flex
        ~~~
    - Download freefem++ at [here](http://www.freefem.org/) (choose the tar.gz file)
    - Extract and `cd` to the extrated folder
    - Run following commands

        ~~~ bash
    autoreconf -i
    ./configure 
    make 
    make check
    sudo make install
        ~~~
32. **Download a direct link by terminal**

	~~~ bash
	wget <direct-link> -O <name-of-file>.<file-extension>
	~~~

33. **Download from google drive by terminal**
	- Download as usual without terminal by a web browser
	- Open Downloads windows of the browser and then copy the download link.
	- Stop the download process
	- Use the command link in 33 where `<direct-link>` is the link copied above.
34. **Unzip**: `sudo apt-get install unzip` and then `unzip <file>` or `unzip <file> -d <destination>`
35. Remove 

	~~~ bash
	rm <file>
	rm -f <file> # force to remove
	rm -rf <dir> # remove folder and files includes
	rmdir <empty-dir> # remove empty directories
	~~~
36. **Check size of a folder**

	~~~ bash
	du -hs <directory>
	~~~

	- "h" : human readable (6.7G)
	- "s" : only this directory (otherwise, it reads all included)

37. **Mount iso file on linux**

	~~~ bash
	sudo mount -o loop <image>.iso /mnt/<folder>
	~~~

	If you mount another iso file to the same <folder>, it will replace the current one.

38. **Extract a iso file**: first, mount it like in 37 to folder named `iso` then copy all the contents in `iso` to some folder you want.

	~~~ bash
	cp -r /mnt/iso <directory>
	~~~

39. **How to install matlab silently** (only with command lines) on linux? (if below doesn't work, you can [cf here](http://installfights.blogspot.com/2016/11/how-to-install-matlab-without-gui.html), my method is different from this one)

	- Suppose that you have 2 dvd iso files which contains the installation of matlab (`dvd1.iso` and `dvd2.iso`)
	- For the activation, you have `libmwservices.so` and `license_standalone.lic`
	- First, you need to extract 2 dvd iso files to a common folder named `install_matlab` in `/home/thi/`
	- Create a new folder to install matlab called `matlabR` in `/home/thi/`
	- Extract all files in 2 iso files to folder `install_matlab` like the instruction 38
	- Run below command line

		~~~ bash
	sudo ./install -agreeToLicense yes -mode silent -destinationFolder /home/thi/matlabR -fileInstallationKey xxxxx-xxxxx-xxxxx  -outputFile /home/matlab_install.log
		~~~

	- After the installation, copy file `license_standalone.lic` to `/home/thi/matlabR/licenses/`
	- Copy file `libmwservices.so` to `/home/thi/matlabR/bin/glnxa64/`
	- Try running matlab: `/home/thi/matlabR/bin/matlab`
	- If you have an error like `libXt.so.6: cannot open shared object file: No such file or directory`, try to install `sudo apt-get install install libxt6`.
	- Make linux recognize your matlab command `matlab` like in the instruction 40.
	- Finish.

40. **Make linux recognize matlab command**

	- Suppose that you have installed matlab on `/home/thi/matlabR`
	- You need to add above directory to the `$PATH` so that the system can recognize your `matlab` command

		~~~ bash
	export PATH=$PATH:/home/thi/matlabR/bin
		~~~
	- You can use `echo $PATH` to check if the path is located in it or not.

41. **Sync files with mega right on terminal**

	- Install **megatools: `sudo apt-get install megatools`
	- Using megatools, cf the [main website](https://megatools.megous.com).
	- Create a condig file which stores your login information (be careful, everyone can see your pass)

		~~~ bash
	sudo apt-get install vim # in case that you don't have vim on your system
	vim .megarc # create a file named .megarc
		~~~

	- `vim` opens and type

		~~~ bash
	[Login]
	Username = your@email
	Password = yourpassword
		~~~

		If you have back slash in your password, you must escape it with another backslash

	- Quit `vim` and save the file by pressing <kbd>ESC</kbd> and then `:wq!`
	- **Upload a file**: `megaput --path /Root/<folder> file`
	- **See the list of file on remote**: `megals`
	- **Upload a folder**: `megacopy --local <folder> --remote <folder>`
	- **Download from link**: `megadl <mega-link>`
	- **Download a single file**: `megaget <file>`
	- **Download from uploaded directory**: `megacopy --local <folder> --remote <folder-to-download> --download`



