---
layout: post
title: install nvidia optimus window manager
categories: [setup]
tags: [gpu, archlinux, nvidia, setup]
fullview: true
---
install driver nvidia (sesuaikan dengan versinya)
{% highlight bash %}
yay -S nvidia-390xx
{% endhighlight %}

install nvidia xrun, karena menggunakan driver berbeda saya hilangan depens nvidia
{% highlight bash %}
yay -G nvidia-xrun-git
{% endhighlight %}

{% highlight bash %}
cd nvidia-xrun-git
{% endhighlight %}

edit PKGBUILD hilangkan 'nvidia' pada option depends

{% highlight bash %}
makepkg -si
{% endhighlight %}

{% highlight bash %}
sudo systemctl enable nvidia-xrun-pm
{% endhighlight %}

{% highlight bash %}
lspci | grep -i nvidia | awk '{print $1}'
04:00.0
{% endhighlight %}

edit /etc/X11/nvidia-xorg.conf
BusID sesuaikan dengan output dari lspci
{% highlight bash %}
Section "Device"
  Identifier "nvidia"
  Driver "nvidia"
  BusID "PCI:4:0:0"
EndSection
{% endhighlight %}

edit /etc/X11/nvidia-xorg.conf.d/30-nvidia.conf
BusID sesuaikan dengan output dari lspci
{% highlight bash %}
Section "Device"
    Identifier "nvidia"
    Driver "nvidia"
    BusID "PCI:4:0:0"
    #  Option "DPI" "96 x 96"
EndSection
{% endhighlight %}

edit file /etc/default/nvidia-xrun
{% highlight bash %}
CONTROLLER_BUS_ID=0000:00:1c.4
DEVICE_BUS_ID=0000:01:00.0
{% endhighlight %}

disesuaikan ouput dari 
{% highlight bash %}
lspci untuk DEVICE_BUS_ID
lshw untuk CONTROLLER_BUS_ID biasanya sebelum graphic card, kalo belum punya lshw install dulu
{% endhighlight %}

copy semua conf yang ada di /etc/X11/xorg.conf.d ke /etc/X11/nvidia-xorg.conf.d

buat nvidia-xinitrc untuk memulai nvidia-xrun

{% highlight bash %}
mkdir -p  ~/.config/X11
{% endhighlight %}

tambahan ke ~/.config/X11/nvidia-xinitrc
{% highlight bash %}
#!/bin/sh
userresources=$HOME/.Xresources
usermodmap=$HOME/.Xmodmap
sysresources=/etc/X11/xinit/.Xresources
sysmodmap=/etc/X11/xinit/.Xmodmap

# merge in defaults and keymaps
if [ -f $sysresources ]; then
    xrdb -merge $sysresources
fi

if [ -f $sysmodmap ]; then
    xmodmap $sysmodmap
fi

if [ -f "$userresources" ]; then
    xrdb -merge "$userresources"
fi

if [ -f "$usermodmap" ]; then
    xmodmap "$usermodmap"
fi

# start some nice programs
if [ -d /etc/X11/xinit/nvidia-xinitrc.d ] ; then
 for f in /etc/X11/xinit/nvidia-xinitrc.d/?*.sh ; do
  [ -x "$f" ] && . "$f"
 done
 unset f
fi

TERM=xterm-256color
LS_COLORS='rs=0:di=01;34:ln=01;36:pi=40;33:so=01;35:do=01;35:bd=40;33;01:cd=40;33;01:or=40;31;01:su=37;41:sg=30;43:tw=30;42:ow=34;42:st=37;44:ex=01;32:';
export LS_COLORS
export PATH="${PATH}:$HOME/.local/bin"
export TERMINAL=urxvt
export ARCHFLAGS="-arch x86_64"
export EDITOR=nano
export VISUAL=nano
export AWT_TOOLKIT=MToolkit
export MSF_DATABASE_CONFIG="$HOME/.msf4/database.yml"
PERL_DESTRUCT_LEVEL=2
export PERL_DESTRUCT_LEVEL
export RXVT_SOCKET="$HOME/.urxvt/urxvtd-`hostname`"

urxvtd &
picom --config ~/.config/picom/picom.conf &
unclutter -root &
xautolock -time 60 -locker blurlock &
dunst &
redshift-gtk &
nm-applet --sm-disable &
blueman-applet &
feh --bg-fill ~/Pictures/wallpaper/wallpaperbetter.jpg &
sxhkd -c ~/.config/sxhkd/sxhkdrc &

[ ! -s ~/.config/mpd/pid ] && mpd

if [ $# -gt 0 ]; then
    $*
else
while true; do
    dwm 2> ~/.dwm.log
done
fi
{% endhighlight %}


edit /etc/pam.d/sudo tambahkan pada baris pertama group wheel sudo tanpa password
{% highlight bash %}
	auth           sufficient      pam_wheel.so trust use_uid
{% endhighlight %}

reboot
login diconsole
ke nvidia => nvidia-xrun
ke intel => startx
