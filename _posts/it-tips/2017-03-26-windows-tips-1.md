---
title: Windows tips 1
description: 
categories:
  - it-tips
type: Document
use_math:
---

## Music on Windows 

### How to uninstall Groove Music on Windows 10

1. Open Windows PowerShell with administrator
2. `Get-AppxPackage –AllUsers`
3. Scroll down and locate Zune Music (yes, it is).
4. Copy the PackageFullName of ZuneMusic using selecting the text next to PackageFullName and using Ctrl+C hotkey.
5. `Remove-AppxPackage PackageFullName`

**Method 2** : using CCleaner > Tools > Uninstall

### Reinstall Windows Media Player

**Step 1.** Uninstalling the Windows Media Player:

1. Go to Start and in the search type "**Turn Windows features On or Off**".
2. Click on "**Turn Windows features On or Off**".
3. Browse to the **Media Features** and uncheck the mark in front of Windows Media Player.
4. Restart the computer

**Step 2.** Reinstalling the Windows Media Player:
1. Go to Start and in the search type "**Turn Windows features On or Off**".
2. Click on "**Turn Windows features On or Off**".
3. Browse to the Media Features and place a check mark in front of Windows Media Player.
4. Restart the Computer.


There is also another alternative choice for you, it's **Groove Music** app.

## HiDPI problem

### Matlab hidpi changes

From Matlab 2015b, if you use the high dpi computer, there is no problem with the display in matlab, everything is ok. However, there is some error if you connect your computer to an external display with lower dpi settings. The font in matlab editor is not good if you see it under external display. In order to adapt with this problem, there are some choices for you

1. If you use with an external lower-dpi, go to matlab installation folder > **bin** > right lick on **matlab.exe** and then choose **Properties** > tab **Compatibilities** > Check on **Override hide DPI scaling behavior. Scaling performed by** and choose **System** in the list.
2. If you only use the computer without any external display, uncheck the above option.

###  Fix scale HiDPI resolution for apps 

For example, app's name is "abc". It locates in C. Create a file with the name "abc.exe.manifest" (all are lower-case) whose content is as in below and then place it in the same folder of file abc.exe. Run again abc and see the result.

```
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>

<assembly xmlns="urn:schemas-microsoft-com:asm.v1" manifestVersion="1.0" xmlns:asmv3="urn:schemas-microsoft-com:asm.v3">

<dependency>
  <dependentAssembly>
    <assemblyIdentity
      type="win32"
      name="Microsoft.Windows.Common-Controls"
      version="6.0.0.0" processorArchitecture="*"
      publicKeyToken="6595b64144ccf1df"
      language="*">
    </assemblyIdentity>
  </dependentAssembly>
</dependency>

<dependency>
  <dependentAssembly>
    <assemblyIdentity
      type="win32"
      name="Microsoft.VC90.CRT"
      version="9.0.21022.8"
      processorArchitecture="amd64"
      publicKeyToken="1fc8b3b9a1e18e3b">
    </assemblyIdentity>
  </dependentAssembly>
</dependency>

<trustInfo xmlns="urn:schemas-microsoft-com:asm.v3">
  <security>
    <requestedPrivileges>
      <requestedExecutionLevel
        level="asInvoker"
        uiAccess="false"/>
    </requestedPrivileges>
  </security>
</trustInfo>

<asmv3:application>
  <asmv3:windowsSettings xmlns="http://schemas.microsoft.com/SMI/2005/WindowsSettings">
    <ms_windowsSettings:dpiAware xmlns:ms_windowsSettings="http://schemas.microsoft.com/SMI/2005/WindowsSettings">false</ms_windowsSettings:dpiAware>
  </asmv3:windowsSettings>
</asmv3:application>

</assembly>
```

### Fix hidpi problem on Windows with external display

If the main screen of your computer has a very high dpi resolution but your external display doesn't. Whenever you connect them and change position of some app. The app's interface is going to be very ugly (and big) in the external display because this app's resolution is fixed in the high dpi.

To fix this problem, you can change the app's setting to the lower dpi so that it adapts well with the external's resolution. The only weakness of this method is that, the app's interface in the main screen is not so good.

Right click on the app's icon/shortcut > choose **Properties** > tab **Compatibilities** > Check on **Override hide DPI scaling behavior. Scaling performed by** and choose **System** in the list.

## How to download unlimited size on Mega?

1. Download [MegaDownloader](https://drive.google.com/open?id=0B7pwkv5Gv-VHRW9xdVk2LW1LSjQ) (it's portable)
2. Install **IDM**
3. Open **MegaDownloader** > **Configuration** > **General** > untick all fields > **Streaming** tab > check **Use streaming server** > **Port** : 54321 > **Save** > If there is a dialogue "**New version available**" > **No**
4. Usage : **Streaming** > **Watch online** > copy mega link and paste to **MEGA URL link** > copy link created after that > Close but NOT exit MegaDownloader > Open IDM > **Add URL** > Download as usual.


## Linux in Windows 10

### Linux Bash shell in Windows 10

1. Open Settings > Update & security > For Developers
2. Under "Use developer feature", select "Developer mode" > Yes > Restart the computer
3. Control Panel > Programs > Turn Windows features on or off 
4. Check on Windows Subsystem for Linux (Beta) > OK > Restart now
   1. Open Bash > Enter > yes > enter UNIX username (don't need to be the same with windows user)

### Open Graphic Linux App in Windows 10

1. Install [Xming Server](https://sourceforge.net/projects/xming/)

2. Run Xming after installing

3. Enter Bash and run the following line AT EACH time you wanna run some app

   ```
   export DISPLAY=:0
   ```

4. Run app from Bash (by command)

### Recover windows bootloader / boot menu after removing Linux

Using a USB 8GB or bigger and then search Recovery Drive in Windows 10.

How to use : [here](http://support.hp.com/us-en/document/c03529751).

### UEFI insead of BIOS boot mode

Enter UEFI mode, go to boot options, delete Ubuntu, that's it.

### Install Ubuntu/Linux on Windows 10

You should use VMWare instead of VirtualBox because VB make Ubuntu very slow in using (still don't know why)

### Share files between Windows and Ubuntu on VMWare

Ref [here](http://theholmesoffice.com/how-to-share-folders-between-windows-and-ubuntu-using-vmware-player/). 

1. Turn off Ubuntu

2. Choose Edit virtual machine settings > Share folders > Always > Add... > Add some folder you want to share

3. Boot to Ubuntu, shared folder will be located at `/mnt/hgfs ` but you will not see it.

4. Run this in Terminal `vmware-hgfsclient`, this will show the folders you have shared

5. Now run `sudo vmware-config-tools.pl`. If there is nothing, we need to install this tool again. Step 6 to 10 will help you to do this, thanks to 

6. In VM windows, choose Player > Manage > Reinstall VMWare Tools... > Ubuntu will mount CDROM containing VMWare Tools. Copy the .tar file to /home/Downloads folder (or anywhere else you want). Extract it and `cd` to it.

7. Go to root `sudo -i`, go to this folder `cd /home/dinhanhthi/Downloads/extracted-folder/`

8. Reject CDROM

9. Run `./vmware-install.pl` and follows step appearing on the screen (choose "yes" for all options).

10. Log out og the root account `exit`

11. Come back to the step 5. Now there will be a folder like `/mnt/hgfs/`, you can `cd` to it to see the shared folder.

12. Now, create a shortcut on desktop pointing to this location by

   ```
   ln -s /mnt/hgfs/shared-directory ~/Desktop/Name-of-the-folder
   ```

13. Voilà, see the Desktop to catch the result you expect.
14. Note : folders need to be shared : www-backup, Data F, C Downloads, Dropbox

## IDEs

### FreeFem++ build system with Sublime Text in Windows 10

1. Open Sublime Text 3

2. Tool > Build system > New build system

3. Create a file with arbitrary name (for example, FreeFemPP), type "sublime-build" and save with the following content

   ```
   {
   	"cmd": ["launchff++","$file"]
   }
   ```

   Please see more [documentation of Sublime](http://docs.sublimetext.info/en/latest/reference/build_systems/configuration.html).

4. Tools > Build system > FreeFemPP

5. Using : Ctrl + B.

### Change syntax highlight for .edp in Sublime Text

Open Sublime Text > View > Syntax > Open all with current extension as... > C++

### Open correctly syntax highlight with some extension in Sublime Text

For example,  I wanna open a matlab file (.m) and I want Sublime Text open this file with the syntax hightlight is in matlab language.

1. Open some matlab file.
2. **View** > **Syntax** > **Open all with current extension as** > **MATLAB**.

After that, in the future, whenever you open a .m file, Sublime will highlight the codes as matlab language for you.

### WinEdt and its options

WinEdt is a good choice, but I recommand you to choose [TexItEasy](https://texiteasy.com). It has a SublimeText-like UI.

#### How to change PDF viewer on WinEdt?

**Options** > **Excution Modes** > **PDF Viewer**

In Sumatra, **Settings** > **Options** and paste the following

```
 "C:\Program Files\WinEdt Team\WinEdt 9\WinEdt.exe" -C="WinEdt 9.1" "[Open(|%f|);SelPar(%l,8);]"
```

#### Open PDF right after execution

**Options** > **Execution Modes** > **Console Applitions** > Choose the right one on “**Accessoires**” and then choose the appropriate ones in “**Process Flow**” > Tich “**Wait for Execution to finish**” and “**Start Viewer**” and “**Forward Search**”

#### Choose small toolbar

Options > Toolbar  > choose what you want

## Document reader

### SumatraPDF

**WinEdt**

```
InverseSearchCmdLine = "C:\Program Files\WinEdt Team\WinEdt 10\WinEdt.exe" "[Open(|%f|);SelPar(%l,8)]"
```

**Sublime** 

```
InverseSearchCmdLine = "C:\Program Files\Sublime Text 2\sublime_text.exe" "%f:%l"
```

~~~
"C:\Program Files\WinEdt Team\WinEdt 10\WinEdt.exe" "[Open(|%f|);SelPar(%l,8)]"
~~~

### How to open Foxit Reader in multi windows

File > Prefernces > Documents > Allow multiple instances.

## Apps & Softs

### How to add French to Babylon 8

Start > Region and language > Language > Add language > Fracncais > Options > Speech > Settings/Download (something like that)  > Come back to Region and language, choose tab Speech > Text-to Speech > Choose Microsoft Paul Mobile (French Voice).

In babylon 8 > Settings > Miscellaneous > Say-it-settings > Voice > Microsoft Hortense Desktop (French). 

You can only use one voice once.

## Troubles & problems

### How to fix to log on to Windows 10 after fail installing “Windows 10 Login Background Changer”

In order to change Windows 10’s logon background, most of website on the internet suggest to use an app called “[Windows 10 Login Background Changer](https://github.com/PFCKrutonium/Windows-10-Login-Background-Changer)“. However, for some new versions of Windows 10, this problem causes a very bad problem on logon screen. You cannot see your logon screen. There is only a cursor on the screen, that’s all. That’s why you cannot log on to your Windows anymore. This post help you to fix this problem.

The problem is worse if you are using dual boot menu between Windows and Linux OS. It’s my problem.

All tools that you need before fixing this problem is

1. USB key 8Gb or bigger.
2. File windows 10 installer (ISO).

**First choice**, use another Windows 10 machine to [create a recovery drive to this USB](https://support.microsoft.com/en-us/instantanswers/3a747883-b706-43a5-a286-9e98f886d490/create-a-recovery-drive). This way is faster.

**Second choice** (I have done in this way), use [Universal USB Installer](https://www.pendrivelinux.com/universal-usb-installer-easy-as-1-2-3/) to make a USB Windows installer drive from above ISO file. This is a portable app, it’s easy to use, don’t worry. This way takes time to install ISO file to USB key (around 15 minutes).

Turn off your computer by press for a very long time the power button.

Next step is **make your computer start from USB**. It’s another tip, I suppose that you know how to do that.

Plug in your USb windows installer, start your computer and make sure that your computer start to Windows Installer.

Click on **Repair your compuer** insead of **Install now**> **Advanced Options** > **Command Prompt. **If you can proceed to this step, everything is almost done.

Next, find your Windows drive letter. Use below command line to list all your Drives letter

```
wmic logicaldisk get name
```

You  can also use this for another option

```
wmic logicaldisk get caption
```

After knowing exact the all drive letters, check each of them to be sure which one Windows are locating on. How to do that? By list all folder/files inside each drive and see what is in it.

```
dir drive-letter:
```

If you can see a folder like “**Program Files**“, it’s the drive you want! Here I suppose your letter is “**F”**.

Type the following cmmand line to go to folder **Windows.UI.Logon**

```
cd F:\Windows\SystemResources\Windows.UI.Logon\
```

Then you need to delete file **Windows.UI.Logon.pri**. Pay attention, it’s neccessary to have another file called **Windows.UI.Logon.prei.bak**

```
del Windows.UI.Logon.pri
```

Then

```
copy Windows.UI.Logon.pri.bak Windows.UI.Logon.pri
```

Reboot and see the changes.

### Problem with Windows Defender

WD is turned off "This app is turned off by group policy"

Ctrl + R > regedit to open Registry Editor > HKEY_LOCAL_MACHINE > Software > Policies > Microsoft > Windows Defender > delete DisableAntiSpyware or change the value to 0 > restart again Windows Defender.

### Some app's windows is overflow the screen

Một vài ứng dụng có cửa sổ tràn khỏi màn hình, làm sao để có thể hiện mấy nút min/max/close?

Nhấn vào **Task View** (Start+Tab) để xem nhanh tất cả các cửa sổ của các ứng dụng > Chuột phải vào ứng dụng đang bị > **Snap left**.

### Hide/Show action center icon on taskbar

1. Press Start button on your keyboard and search “**Local Group Policy Editor**” to open it. Another way to open LGP is press Windows+R and type into the Run diabox “**gpedit.msc**“
2. In the left pane > User Configuration > Administrative Template > Start Menu and Taskbar > Remove Notification and Action Center > Double click on it > Choose “diable” if you wanna the icon to appear and “enable” if you don’t. Note that, on some website, they say the contrary.
3. Restart the computer to see the result.

### Chrome tự động chuyển sang thư mục khác

Một con spyware hay virus gì đấy, tự động copy chrome sang một thư mục khác, chuyển đổi hết trong registry luôn. Dưới đây là kinh nghiệm phòng tránh, chưa biết cách diệt.

- Trong Chrome, mở [chrome://version/](chrome://version/) để biết là đang mở chrome từ thư mục nào.
- Tìm trong windows Explorer hết tất cả các tên liên quan và xóa đi các thư mục tương ứng, thường nó nằm trong Appdata.
- Dùng ứng dụng regscan để quét hết các registry, xóa hoặc thay bằng chrome chính chủ.
- uninstall và cài lại chrome mới. Phát hiện ra là sau khi cài IDM và its extension mới bị nhưng không chắc.

## Browsers

### Change default browser in Cortana into Chrome

#### Method 1 : change default browser and search engine

1. From [this help](http://www.winhelponline.com/blog/cortana-web-results-google-search-default-browser/).
2. Download [this tool](https://drive.google.com/open?id=0B7pwkv5Gv-VHVk00ZURic21fRFE).
3. Run cortana_default_browser.reg
4. Copy cortana_default_browser.vbs into C:\Windows
5. Open Edge > Settings > Advanced > Turn on Optimize taskbar web search results…
6. Try Cortana and see the results

#### Method 2 : only change the default browser in Corana (cannot change the search Engine)

1. The guide follows [here](http://www.makeuseof.com/tag/force-cortana-use-chrome-google-windows-10/).
2. Download [SearchWithMyBrowser](https://github.com/charlesmilette/SearchWithMyBrowser) and then save this extracted folder in a safe place because we will need it permanently (Document, forexample).
3. Run make batch file and then run install batch file. 
4. After running install batch file, a cmd windows will appear, in this windows, it needs you to paste a path
5. Come bacm to SearchWithMyBrowser folder, press Shift + right click on SearchWithMyBrowser.exe > Copy as path > go to cmd windows, right lick to paste the path
6. Hit Enter, a confirm appear which asks you to choose, then choose SearchWithMyBrowser.exe.
7. Try search anything with Cortana, choose SearchWithMyBrowser.exe again (tick on Using this forever or something like that for the future uses)

### Disable history on search bar Google Chrome

To disable omnibox suggestions in Google Chrome, follow these steps:

1. In a Chrome window, click the menu icon in the upper-right, which looks like three vertical dots ( **⋮** ). (If you're using Mac OS X, open the Chrome menu at the top of your screen.)
2. Select **Settings**. (If you're using Mac OS X, select **Preferences**.)
3. Scroll down and click **Show advanced settings...**
4. Under **Privacy**, deselect the box labeled **Use a prediction service to help complete searches and URLs typed in the address bar**.

And then clear all the history

### Stop open automatically downloaded PDF files in Google Chrome

Options > Advanced > Click on Clear Auto opening settings

### Delete suggested url on address bar Chrome, Firefox

When you type something on the address bar, you will see unexpected urls appearing on the suggested list below. Use the arrow key to navigate to the url that you wanna delete and then press **Shift + Del** (Chrome/Firefox on Windows) or **Fn + Shift + Del**(Chrome/Firefox on MacOS)

For Internet Explorer (IE), whenever the suggested url appear, move your mouse over this url, a “x” symbol will appear on the right of this, just click on it, the url will be delete.

## How to Find Windows Spotlight Lock Screen Images in Windows 10

First, you need to enable Windows Spotlight Lock Screen on your computer : **Start** > **Settings** > **Personalization** > **Lock Screen** > choose **Windows Spotlight**

Enable view hidden files in Windows Explorer : Open **Windows Explorer** > **Tab View** > Tick on **Hidden items**

Navigate to the folder containing photos: **C** > **Users** > **[Your-user-name]** > **AppData** > **Local** > **Packages** > **Microsoft.Windows.ContentDeliveryManager_cw5n1h2txyewy** > **LocalState** > **Assets**

Rename all files in the **Assets** folder from **abc**, for example, to **abc.jpg** and done!

## File managers

### Change a part of name multiple files

Muốn đổi 1 phần tên hàng loạt file, ví dụ muốn xóa chữ `"WWW.NHACSO.NET-` trong tất cả các tên file thì dùng **PowerShell** `cd` đến thư mục đó (cũng có thể mở PS lên, gõ `cd ` xong dùng Explorer kéo thả thư mục đó vào để tự động điền đường dẫn)

~~~
get-childitem *.mp3 | foreach { rename-item $_ $_.Name.Replace("WWW.NHACSO.NET-", "") }
~~~

### Add new item in context menu New

Create a file whatever-name.reg with following content

```
Windows Registry Editor Version 5.00

[HKEY_CLASSES_ROOT\.md\ShellNew]
"NullFile"=""
```

Replace "md" with other extensions.

### How to know what is using some file/folder in Windows?

Sometimes you cannot delete some file/folder in Windows with the caution “The file/folder is used by some process/app”. You need to know exactly what app which is using this file/folder to turn it off.

[Lock Hunter](https://lockhunter.com/) soft will help you to do that, it also help you delete file/folder you want.

I have a problem with taskbar search after installing some apps (specifically, it’s advanced system care free edition) and disable (and re-enable) Windows search system service. I have found the solution for this case, it comes from [windowscentral](http://www.windowscentral.com/how-fix-taskbar-search-not-working-windows-10).

### Taskbar search is not working in Windows 10

**Method 0. Be sure that Windows Search service is running and enable.** Open services manager (Press the same them Start + R > type “**msconfig**” > Choose tab “**services**” and locate Windows Search services and enable it > restart your computer)

**Method 1**. **Restart Cortana in Task Manager** : right click on Start button > **Task Manager** > Find and End task with Cortana (it will automatically reopen). the problem with search on taskbar will be solved.

**Method 2**. If above method doesn’t work for you. **Try to restart Windows Explorer**. In order to do that, the same way with Cortana to End Task but to open it again, you need more step. In Task Manager windows, click on  **File** > **Run new task** > type “**explorer**” and hit Enter.

**Method 3. Use Windows troubleshooter to restore indexing services.** Right click on Start button > **Control Panel** > **Category** (near the top right corner of the windows) > Large icon > **Troubleshooting** > **System and Security** > Right click on **Search and Indexing** > **Run as administrator** > **Next** > click the check box next to any problems you’re encountering, in this case just click **Files don’t appear in search results** > **Next** (troubleshooter will do the remaining job)

**Whatever method you choose, just to be sure that you need to restart your computer to see the changes.**

## How to turn localhost in Windows

In this post, I will show how to turn on localhost in Windows so that you can build your own localhost website and can go to **http://localhost/yoursite.html** to check what will happen before uploading to the real host. I will also show you where the locaohost folder located in your Windows folders. This method works for **Windows 7 and later**.

In order to active localhost, go to **Control Panel** > **Program and Features** > **Turn Windows features on or off** > locate **Internet Information Services** and check its check box > **OK/Apply**. You don’t need to restart your computer.

In your browser, navigate to **http://127.0.0.1/** or **http://localhost/** to see what happens.

You can find your localhost folder in `C:\inetpub\wwwroot\`

