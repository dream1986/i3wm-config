[English introduction](README-en.md)

---

![](arch-i3.jpg)

# 安装配置

## 安装软件

- 基本
  - `i3 `：某些发行版中`i3`可能为一个包组名，它包含i3窗口管理器和其他组件，`i3-wm` 、 `i3-gaps`、 `i3block` 、 `i3lock`和`i3status`，另一些发行版中`i3`也可能仅为wm部分。（可在[pkgs.rog](https://pkgs.org)搜索关键字以确定包名）
  - 适合的终端（参照下文[终端](#终端) 选择一个终端）
  - `dmenu`  程序启动器
  - `feh`  设置壁纸
- 可选
  - `xcompmgr`     终端透明
  - `scrot`   截屏（本配置使用的截屏快捷键调用此工具）
  - `pcmanfm`    文件管理器
  - `networkmanager`用户
    - `nm-connection-editor`  图形界面的联网管理工具
    - `nm-applet`  托盘图标
  - 笔记本用户
    - `mate-power-manager`  电源管理工具
    - `alsa-utils`   声音管理

## 配置i3

- 下载本配置文件并解压，将i3和i3status放于`~/.config/`目录，将`Pictures`（包含几张示例壁纸）放于当前用户家目录下（即`~/`下）。如果需要显示托盘图标，可能需要参考后面[托盘图标](#托盘图标)一小节的内容进行相关配置。

或者

- 直接执行：

```shell
curl -# -L -o i3.zip https://github.com/levinit/i3wm-config/archive/master.zip && unzip i3.zip && cd i3wm-config-master && cp i3 i3status -t ~/.config -r && cp Pictures ~/ -r && ./config-zh.sh
```

如果提示`xrandr: command not found`，则需要先安装`xorg-xrandr`在执行上述命令。

# 本配置的说明

关于本配置的一些重要说明。
## 快捷键
以下列出此配置文件的自定义快捷键的说明，未作更改的其他i3wm的默认快捷键请参阅i3wm相关文档或查看config文件。

快捷键在默认配置上稍作修改，参照了windows下的常用快捷键和vim操作习惯。

`$mod key`使用的默认的Mod4，**一般指的是**windows键或super键或meta键。


- 截图

  `$mod+PrtSc`（配置里绑定的是scrot截屏工具，**需要安装scrot**，PrtSc即PrintScreen键）

- 文件管理器

  `$mod+e`（配置里使用的lxde桌面pcmanfm文件管理器，e-explore）

- 关闭窗口

  `Alt+F4`（Alt一般是mod1键）

- 隐藏和再现窗口

  `$mod+minus`和`mod+plus`（minus即是减号所在键，plus即是加号所在键）

- 调整窗口边框风格
  - `$mod+n`  有边框和标题栏（n-normal）
  - `$mod+u`  无边框和标题栏（默认，u-unnormal）
  - `$mod+o`  1像素边框（o-one pixel）
  - `$mod+b`   可在上面三种风格来回切换（b-border style）

- 窗口平铺模式

  - `$mod+s`  堆叠式（s-stacking）
  - `$mod+t`  标签式（t-tab）
  - `$mod+c`  在垂直平铺和水平平铺之间来回切换（默认，c-change）

- 切换焦点窗口
  `$mod+h/j/k/l`或者`$mod`+上下左右箭头

- 移动焦点窗口（平铺模式）
  `$mod+Shift+h/j/k/l`或者`$mod+shift`+上下左右箭头

- 分割窗口
  - `$mod+v`    垂直分割（v-vertical）。
  - `$mod+Shift+h`   水平分割（默认风格，h-horizon）。

- 相邻工作区切换


  - `$mod+tab`    后一个
  - `alt+tab`    前一个

- 重启和重载i3

  - `$Mod+Shift+s`  -- 重载i3配置（修改过配置文件后使用该操作）
  - `$Mod+Shift+r`  -- 重启i3

- 锁屏/关机/重启/退出 菜单：按下`$mod+shift+q` 唤出该菜单，然后按下：


  - `l`    锁屏
  - `p`    关机
  - `r`    重启
  - `e`    退出i3

- 亮度和音量（笔记本）

  - 音量
    - `Fn`+音量加减键或静音（荧幕不会出现提示，可参看bar上的显示）
    - `alsamixer`（需要`alsa-utils`）
  - 亮度：`Fn+亮度加减键`（需要电源管理软件，推荐**mate-power-manager**）

  注：也可能不需要按下fn键，这和其BIOS中是否设置了需要fn辅助按键有关。

## 壁纸和锁屏
- 壁纸

  随机模式是本配置的默认模式，它使用了 [i3/wallpaper.sh](i3/wallpaper.sh) 这个脚本。编辑  [i3/config](i3/config) 文件可切换模式。

  - 随机模式：自动切换壁纸，将要用作壁纸的图片放到`~/Pictures/wallpapers` 即可。
  - 静态模式：使用一张图片作壁纸，图片路径是`~/Pictures/wallpaper/wallpaper.jpg` 。

- 锁屏

  - 图片路径是`~/Pictures/wallpaper/lock/lock.jpg`
  - 使用``$mod+alt+l` 锁屏
  - 解锁：输入用户密码再按回车键即锁屏。

*建议用一个固定的路径设置壁纸或锁屏，需要更换壁纸的时候将新图片命名位wallpaper放进去覆盖即可，这样比较方便（当然要注意后缀名是否一致）。*


## 电源管理
在 [i3/config](i3/config) 配置中有一行：

> exec --no-startup-id xset dpms 333 666

意思是系统闲置333秒后灭屏，666秒后系统挂起。根据自己需要进行修改。

你也可以使用mate-power-manager或者其他电源管理工具。



一些有关电源管理的参考信息：

- [电源管理](https://wiki.archlinux.org/index.php/Power_management_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87))
- [linux笔记本相关](https://github.com/levinit/itnotes/blob/master/linux/laptop%E7%AC%94%E8%AE%B0%E6%9C%AC%E7%9B%B8%E5%85%B3.md)
- [挂起、睡眠和休眠](https://wiki.archlinux.org/index.php/Suspend_hybrid-sleep_and_hibernate_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87))


## 终端

如果需要终端背景透明的要过，需要安装xcompmgr（或者compton）。推荐选择可以较为方便设置透明度的终端如roxterm、xfce-terminal和terminator。

最好使用下面的终端之一。按下 $mod+Return，便会启动 i3-sensible-terminal，即执行虚拟终端的脚本。

它会试图按以下顺序一一执行，直到成功启动某虚拟终端（参看 [i3wm-termial](http://jlk.fjfi.cvut.cz/arch/manpages/man/i3-sensible-terminal.1)）： 

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

## 托盘图标
打开 [i3/config](i3/config) ，找到这行

> exec --no-startup-id xrandr --output eDP1 --primary

其中eDP1是我的计算机的显示设备的名字。使用`xrandr`查看计算机显示设备名称。

例如我的显示内容有：

```shell
Screen 0: minimum 8 x 8, current 1920 x 1080, maximum 32767 x 32767
eDP1 connected 1920x1080+0+0 (normal left inverted right x axis y axis) 310mm x 170mm
```



其中的`eDP1`便是我的显示设备名称。如果你的显示设备名称不是`eDP1` ，那么需要修改`exec --no-startup-id xrandr --output eDP1 --primary`这行中`eDP1`为你的显示设备的名字。

或者你可以尝试使用一下命令自动修改：

```shell
name=`xrandr | sed -n '2p' | cut -d ' ' -f 1`
sed -i 's/eDP1/'"$name"'/' ~/.config/i3/config
```

如果提示`xrandr: command not found`，则需要先安装`xorg-xrandr`在执行上述命令。

# 其他提示

- 无法显示emoji图标需安装相关字体包如`fonts-symbola`（也可能名为`ttf-symbola`）
- pcmanfm的垃圾桶功能需安装`gvfs`
- 挂载mtp设备安装`gvfs-mtp`或`libmtp`(参考[archwiki:MTP](https://wiki.archlinux.org/index.php/MTP_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)#.E5.AE.89.E8.A3.85))
- 更改主题可使用lxappearance
- 文字过小或过大可使用lxappearance
- 高分辨显示器缩放问题（参考[archwiki:HIDPI](https://wiki.archlinux.org/index.php/HiDPI#X_Resources))

在用户目录下编辑（如果没有则新建）`~/.Xresources`，添加以下内容：
>Xft.dpi: 144
>Xft.autohint: 0
>Xft.lcdfilter:  lcddefault
>Xft.hintstyle:  hintfull
>Xft.hinting: 1
>Xft.antialias: 1
>Xft.rgba: rgb

其中第一行的Xft.dpi: 144就是dpi，根据实际情况调整大小。 保存该文件，然后在~/.xinitrc写入。

>xrdb -merge ~/.Xresources

当然高分屏下文字过小，也可以适当调整字体大小（可以使用lxappearance）。

- 关闭警告声（alarm sound/beep/蜂鸣）
  参考[PC speaker](https://wiki.archlinux.org/index.php/PC_speaker),方法多样,如：
  `echo "blacklist pcspkr" > /etc/modprobe.d/nobeep.conf`
  或
  `amixer set channel 0% mute`(安装alsa-utils)
  或
  `echo xset -b >> /etc/xprofile`