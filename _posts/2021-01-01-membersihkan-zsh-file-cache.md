---
layout: post
title: menghapus histori zsh file & cache
categories: [how]
tags: [archlinux, zsh, clear]
description: membersihkan histori zsh, file yang telah digunakan & cache
---
membersihkan histori zsh
{% highlight bash %}
cat /dev/null > ~/.zsh_history
{% endhighlight %}

membersihkan file yang telah dibuka 
{% highlight bash %}
rm ~/.local/share/recently-used.xbel
{% endhighlight %}

membersihkan dot cache
{% highlight bash %}
sudo du -sh ~/.cache/ && sudo rm -rf ~/.cache/*
{% endhighlight %}

