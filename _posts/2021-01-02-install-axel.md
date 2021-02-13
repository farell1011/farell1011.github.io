---
layout: post
title: install axel & reflector
categories: [how, setup]
tags: [archlinux, axel, pacman]
description: install axel & reflector untuk mempercepat proses pengunduhan & upgrade system
---

install axel & reflector untuk mempercepat proses pengunduhan & upgrade system
{% highlight bash %}
sudo pacman -S axel reflector
{% endhighlight %}

edit /etc/pacman.conf
{% highlight bash %}
sudo nano /etc/pacman.conf
{% endhighlight %}

dengan menambahkan baris berikut ke bagian **[options]**:
{% highlight bash %}
XferCommand = /usr/bin/axel -n 4 -v -a -o %o %u
{% endhighlight %}

backup mirrorlist
{% highlight bash %}
sudo cp /etc/pacman.d/mirrorlist /etc/pacman.d/mirrorlist.backup
{% endhighlight %}

update mirrorlist dengan reflector
{% highlight bash %}
sudo reflector --score 100 --fastest 25 --sort rate --verbose --save /etc/pacman.d/mirrorlist
{% endhighlight %}

upgrade system
{% highlight bash %}
sudo pacman -Syu
{% endhighlight %}
