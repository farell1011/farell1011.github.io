---
layout: post
title: uefi secure boot di archlinux
categories: [setup]
tags: [archlinux, secureboot, setup]
fullview: true
---
Install toolsnya
{% highlight bash %}
sudo pacman -S efibootmgr
yay -S sbsigntools efitools secure-boot-git
{% endhighlight %}

Creating keys
{% highlight bash %}
sudo secure-boot gen-keys
{% endhighlight %}

Signing EFI binaries
{% highlight bash %}
sudo secure-boot update
{% endhighlight %}
(kalo partion /boot penuh; uninstall systemdboot; sudo bootctl remove; lalu ulangi lagi; sudo secure-boot update) 

install boot entries untuk secure boot
{% highlight bash %}
sudo secure-boot install
{% endhighlight %}

copy key ke boot partisi
{% highlight bash %}
sudo cp /etc/secure-boot/{PK.auth,db.esl,KEK.esl} /boot
{% endhighlight %}

copy cmdline ke /etc/kernel/cmdline
{% highlight bash %}
sudo cat /proc/cmdline > /etc/kernel/cmdline
{% endhighlight %}

tambahakan entrie key tool
(kalo systemdboot diuninstall; install lg; sudo bootctl install)
{% highlight bash %}
sudo cp /usr/share/efitools/efi/KeyTool.efi /boot
{% endhighlight %}

{% highlight bash %}
sudo nano /boot/loader/entries/keytool.conf
{% endhighlight %}

{% highlight bash %}
title  KeyTool
efi    /KeyTool.efi
{% endhighlight %}

reboot ke firmware setup
{% highlight bash %}
sudo systemctl reboot --firmware-setup
{% endhighlight %}

{% highlight bash %}
Security => Restore Factory Keys (Enter)
Security =>Reset to Setup Mode (Enter)
Boot => rubah boot order ke Linux (systemd)
Exit => save & exit
{% endhighlight %}

Enrolling keys in firmware; boot ke key tool tambahkan key
{% highlight bash %}
Edit Keys
DB add key => db.esl
KEK add key => kek.esl
PK add key => pk.auth
(PK harus terakhir ditambahkan)
exit
reboot ke firmware setup
{% endhighlight %}

Enable Secure boot
{% highlight bash %}
Security => enable secure boot
Boot => rubah boot order ke SecureBoot linux
Exit => OS Optimized Defaults (win8 / pure uefi) jika ada (jangan Other OS)
Exit => save & exit
{% endhighlight %}

cek secure boot
{% highlight bash %}
bootctl status
Secure Boot: enabled
{% endhighlight %}

remove systemd bootloader, PK.auth & *.esl file dipartisi boot)
{% highlight bash %}
sudo bootctl remove
cd /boot
sudo rm {PK.auth,db.esl,KEK.esl,KeyTool.efi}
sudo rm -rf loader
{% endhighlight %}
