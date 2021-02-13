---
layout: post
title: setup postgresql
categories: [how, setup]
tags: [archlinux, postgresql, setup]
description: install dan setup postgresql serta perintahnya
---

instal dan setup postgresql serta perintahnya

{% highlight bash %}
sudo pacman -S postgresql
{% endhighlight %}

Initial configuration :
{% highlight bash %}
sudo -iu postgres
{% endhighlight %}

{% highlight bash %}
initdb --locale=en_US.UTF-8 -E UTF8 -D /var/lib/postgres/data
{% endhighlight %}

{% highlight bash %}
exit
{% endhighlight %}

{% highlight bash %}
sudo chown -R postgres:postgres /var/lib/postgres/data
{% endhighlight %}

start postgresql
{% highlight bash %}
sudo systemctl start postgresql.service
{% endhighlight %}

login postgres
{% highlight bash %}
sudo -u postgres -i psql
{% endhighlight %}

membuat user dengan password
{% highlight bash %}
create user msf with encrypted password 'passwordpsql';
create database msfdb;
grant all privileges on database msfdb to msf;
{% endhighlight %}

menampilkan daftar user
{% highlight bash %}
\du
{% endhighlight %}
 
menampilan kewenang user
{% highlight bash %}
\du nama_user;
{% endhighlight %}

menampilan daftar databases
{% highlight bash %}
\l
{% endhighlight %}
keluar postgresql
{% highlight bash %}
\q
{% endhighlight %}


<table>
<colgroup>
<col width="60%" />
<col width="40%" />
</colgroup>
<thead>
<tr class="header">
<th>perintah</th>
<th>keterangan</th>
</tr>
</thead>
<tbody>
<tr>
<td markdown="span">**ALTER USER role_specification;**</td>
<td markdown="span">Mengubah Izin Pengguna yang Ada</td>
</tr>
<tr>
<td markdown="span">**ALTER USER [user] WITH CREATEDB;**</td>
<td markdown="span">Menetapkan Izin</td>
</tr>
<tr>
<td markdown="span">**DROP USER [user];**</td>
<td markdown="span">Perintah untuk Menghapus Pengguna</td>
</tr>
<tr>
<td markdown="span">**DROP DATABASE [database_name];**</td>
<td markdown="span">Perintah untuk Menghapus database</td>
</tr>
</tbody>
</table>
