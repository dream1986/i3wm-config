**[中文介绍](README-zh-CN.md)**

---

![](arch-i3.jpg)

# install & configure

## install softwares

- base

  -  `i3` : in some distros, `i3` is a group name, it contains i3 wm and other compoents, `i3-wm` , `i3-gaps`, `i3block` , `i3lock`and`i3status`, and in other distros, `i3` may be only window manager(wm). (you can search keywords in [pkgs.org](https://pkgs.org))
  -  a terminal  (see [terminal](#terminal), select a terminal emulator ) 
  -  `dmenu`  -- a generic menu for X (like a applications launcher)
  -  `feh`  -- image viewer , for display wallpaper

- optional

  - `xcompmgr`   --  terminal transparent

  - `scrot`  -- for screeshot (this configuration added shortcut for scrot)

  - `thunar` or `pcmanfm`  -- a gui file manager

   - for `networkmanager` user
      - `nm-connection-editor`   -- networkmanager GUI
      - `nm-applet`  -- networkmanager's tray icon

  - `blueman`  bluetooth gui tool

      include a applet `blueman-applet`

  - `mate-power-manager`  -- power manager tool

  - `alsa-utils`  -- adjust volume

  - `xfce4-appfinder`   an application finder

## configure i3

- Downlod this config and extra ,  put `i3` and `i3status` in`~/.config/` , put `Pictures`(contains some sample wallpapers) in home folder (`~/`).If you want display tray icon , Perhaps you should read the chapter -- ["tray icons"](#tray icons).

  optional: exec `config-en.sh` for some basic configuration.

or 

- execute this command:

  ```shell
  curl -# -L -o i3.zip https://github.com/levinit/i3wm-config/archive/master.zip && unzip i3.zip && cd i3wm-config-master && unzip Pictures.zip && cp -r i3 ~/.config && cp -r Pictures ~/ && chmod +x *.sh && ./config.sh
  ```

If it show `xrandr: command not found` , install `xorg-xrandr` , then excute commands above again.

# Introductions for the configs

some info about these config files.



## shortcuts
In configuration, `$mod key` is `Mod4`，**Generally** ,it is "Windows logo" key  or "Super" key, `Alt` is `mod1`, Enter is `Return`.

Tip:Install `xorg-xev`, exec command `xev` in terminal, then press key, it will show the name.

- `Super`+`d`  dmenu
- `Super`+`Enter`  open default [terminal](#terminal)

For other i3wm default shortcuts , see the  **i3wm related documentation** or view the config file.

---



The following are the custom shortcuts in this configuration file(Reference vim and windows usage habits).

- `Super`  temporary display the i3bar
- `Super`+`m`  toggle i3bar show/hideen mode

- xfce dropdown terminal  `Alt`+`/`

  if your default terminal is xfce-terminal

- xfce4-appfinder  `Super`+`a`

  need install the application


- screenshot (full screen)  `Super`+`PrtSc`

    "PrtSc" is "PrintScreen" key , need `scrot`.

- open filemanager  `Super`+`e` 

    need `thunar`（e-explore）

- close window  `Alt`+`F4` 

- hide window and show the hide window `Super`+`minus` and `Super`+`plus` 

    "minus" is "-" key ,and "plus" is "+" key. Here, in order to avoid confusion with +, the name is described in English.

- change window style：
  - `Super`+`n`   with border and title bar (default , **n**ormal)
  - `Super`+`u`    without boder and title bar (**u**nnormal )
  - `Super`+`o`    one pixel boder and no title bar (**o**ne pixel border )
  - `Super`+`b`    change border style in above 3 styles（**b**order style)

- window tilling mode

  - `Super`+`s`    stack mode（**s**tack）
  - `Super`+`t`    tabbed mode（**t**abbed）
  - `Super`+`c`   **change** tile mode betwen horizontal mode and vertical mode (default ,**c**hange | or **c**arvel built :D ）。

- switch focus window

   `Super`+`h` or `j` or `k` or `l`
    or
    `Super`+arrow keys

- move focus window (tiling style)

  `Super`+`Shift`+`h` or `j` or `k` or `l`
  or
  `Super`+`Shift`+ arrow keys

- separate window
  - `Super`+`v`    vertical mode (**v**ertical)
  - `Super`+`Shift`+`h`   horizon mode (default , **h**orizon)

- workspace switching


  -  `Super`+`tab`  -- next
  -  `Alt`+`tab`  -- previous

-  reload and restart i3wm

     -  `Super`+`Shift`+`s`  -- reload i3wm config
     -  `Super`+`Shift`+`r`  -- restart i3wm

-  lock/poweroff/rebot/exit menu : `Super`+`Shift`+`q` it will show a message ,then press


  - `l`  -- lock screen
  - `p`  -- poweroff
  - `r` -- reboot
  - `e` -- exit (i3wm)
- adjust the volume and brightness ( for laptop)

  - volume
    - `Fn` and volume key 
    - use `alsamixer` (need alsa-utils)

    - `Fn` and brightness key （need a power manager tool , recommend `mate-power-manager`)

  tip: maybe `Fn` is not necessary.

## wallpaper and lock screen
- wallpaper

  Random mode is default , it use a script , see [i3/wallpaper.sh](i3/wallpaper.sh) . Edit [i3/config](i3/config) for changing mode.

  - random mode : random switching wallpaper, put pictures in `~/Pictures/wallpapers` .
  - static mode : one pictures as a wallpaper , path is  `~/Pictures/wallpapers/wallpaper.jpg`

- lock screen

  - background path :  `~/Pictures/wallpaper/lock/lock.jpg`
  - lock : `Super`+`Alt`+`l` 
  - unlock : input your user password , then press "Enter" key .


## power management
see [i3/config](i3/config) , it has a line , you can adjust the seconds :

> exec --no-startup-id xset dpms 333 666

In idle state , screen will turn off after 333 seconds , system will suspend after 666 seconds.

You can also use `mate-power-manager` (or other tool) for power management.



see more info about power management:

- [power-management](https://wiki.archlinux.org/index.php/Power_management)
- [laptop](https://wiki.archlinux.org/index.php/Laptop)
- [suspend and hibernate](https://wiki.archlinux.org/index.php/Power_management/Suspend_and_hibernate)

## terminal

If you want a transparent background terminal , need install a  compositor such as  `xcompmgr` (or `compton`  .etc )  .  I recommend some terminal emulators are easy to set a transparent background :`roxterm` , `xfce4-terminal` , `terminator` .

After press terminal shortcut,  It tries to start one of the following (in that order, see [i3wm-termial](http://jlk.fjfi.cvut.cz/arch/manpages/man/i3-sensible-terminal.1)):

>$TERMINAL (this is a non-standard variable)
>
>x-terminal-emulator (only present on Debian and derivatives)
>
>urxvt
>
>rxvt
>
>termit
>
>terminator
>
>Eterm
>
>aterm
>
>uxterm
>
>xterm
>
>gnome-terminal
>
>roxterm
>
>xfce4-terminal
>
>termite
>
>lxterminal
>
>mate-terminal
>
>terminology
>
>st
>
>qterminal
>
>lilyterm
>
>tilix
>
>terminix
>
>konsole

## tray icons

Open [i3/config](i3/config) , find this line :

> exec --no-startup-id xrandr --output eDP1 --primary

eDP1 is the display device's name , you can use `xrandr`  to get your display device's name .

 this is my display device info:

```
Screen 0: minimum 8 x 8, current 1920 x 1080, maximum 32767 x 32767
eDP1 connected 1920x1080+0+0 (normal left inverted right x axis y axis) 310mm x 170mm
```

so , **eDP1** is my display device's name , if your display device's name is not **eDP1** , you should modify this line `exec --no-startup-id xrandr --output eDP1 --primary` ，use your display device's name instead of `eDP1`.



Or you can try these comands for modification:

```shell
name=`xrandr | sed -n '2p' | cut -d ' ' -f 1`
sed -i 's/eDP1/'"$name"'/' ~/.config/i3/config
```

If it show `xrandr: command not found` , install `xorg-xrandr` , then excuted commands above again.

# Other Tips

- not found this package while installing

  Maybe this package  is another name on your distribution. Using the fuzzy search in your pckage manger, also search the real name in this site https://pkgs.org.

- emoji need a font such as `fonts-symbola ` (perhaps its name is `ttf-symbola`)


- `thunar` /`pcmanfm` can not use Trash :  install `gvfs`
- mount MTP divice or other removable disk : install `gvfs-mtp` or `libmtp`(see[archwiki:MTP](https://wiki.archlinux.org/index.php/MTP) )
- change the window/icon/cursor theme or font : `lxappearance` (recommend)
- notfity popup box: `xfce4-notifyd`
- high DPI devices (see[archwiki:HIDPI](https://wiki.archlinux.org/index.php/HiDPI#X_Resources))

edit `~/.Xresources` add (example) :

>Xft.dpi: 144
>Xft.autohint: 0
>Xft.lcdfilter:  lcddefault
>Xft.hintstyle:  hintfull
>Xft.hinting: 1
>Xft.antialias: 1
>Xft.rgba: rgb

144 is dpi (adjust according to the actual display situation).Then edit`~/.xinitrc` , add :

>xrdb -merge ~/.Xresources

- turn off waring sound（alarm sound/beep sound）
  see[PC speaker](https://wiki.archlinux.org/index.php/PC_speaker) 
  `echo "blacklist pcspkr" > /etc/modprobe.d/nobeep.conf`
  or
  `amixer set channel 0% mute`(need `alsa-utils`)
  or
  `echo xset -b >> /etc/xprofile`