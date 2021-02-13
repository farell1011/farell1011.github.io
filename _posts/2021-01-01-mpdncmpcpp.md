---
layout: post
title: setup mpd & ncmpcpp
categories: [setup]
tags: [archlinux, mpd, ncmpcpp, setup]
description: Setup mpd & ncmpcpp
---

install mpd & ncmpcpp
![ncmpcpp](/assets/media/ncmpcpp-mpd.png)


{% highlight bash %}
sudo pacman -S mpd ncmpcpp
{% endhighlight %}

{% highlight bash %}
mkdir -p /.config/mpd
{% endhighlight %}

{% highlight bash %}
mkdir -p /.mpd/playlists
{% endhighlight %}

{% highlight bash %}
nano /.config/mpd/mpd.conf
{% endhighlight %}

{% highlight bash %}
{% raw %}
music_directory		"~/Music"
playlist_directory	"~/.mpd/playlists"
db_file			"~/.mpd/database"
log_file		"syslog"
pid_file		"~/.mpd/pid"
state_file		"~/.mpd/state"
sticker_file		"~/.mpd/sticker.sql"

bind_to_address	"localhost"
port		"6600"
auto_update	"yes"

input {
        plugin "curl"
}

mixer_type	"software"

audio_output {
	type	"alsa"
	name	"ALSA sound card"
}

audio_output {
        type	"pulse"
        name	"pulse audio"
}

audio_output {
    type	"fifo"
    name	"my_fifo"
    path	"/tmp/mpd.fifo"
    format	"44100:16:2"
}
{% endraw %}
{% endhighlight %}

{% highlight bash %}
mkdir -p .ncmpcpp/lyrics
{% endhighlight %}

{% highlight bash %}
nano .ncmpcpp/config
{% endhighlight %}

{% highlight bash %}
{% raw %}
ncmpcpp_directory = "~/.ncmpcpp"
lyrics_directory = "~/.ncmpcpp/lyrics"
mpd_host = "localhost"
mpd_port = "6600"
mpd_music_dir = "~/Music"
audio_output {
        type	"fifo"
        name	"Visualizer feed"
        path	"/tmp/mpd.fifo"
        format	"44100:16:2" 
        }
visualizer_fifo_path = "/tmp/mpd.fifo"
visualizer_output_name = "my_fifo"
visualizer_in_stereo = "yes"
visualizer_sync_interval = "30"
visualizer_type = "spectrum"
visualizer_look = "▋▋"
song_list_format = "{%a - }{%t}|{$8%f$9}$R{$3(%l)$9}"
now_playing_prefix = "─>"
selected_item_prefix = "* "
playlist_display_mode = "classic"
browser_display_mode = "classic"
search_engine_display_mode = "classic"
discard_colors_if_item_is_selected = "no"
incremental_seeking = "yes"
seek_time = "1"
autocenter_mode = "yes"
centered_cursor = "yes"
progressbar_look = "─>─"
default_place_to_search_in = database
user_interface = "classic"
header_visibility = "yes"
statusbar_visibility = "yes"
titles_visibility = "yes"
header_text_scrolling = "yes"
cyclic_scrolling = "yes"
lines_scrolled = "2"
jump_to_now_playing_song_at_start = "yes"
regular_expressions = "extended"
mouse_support = yes
mouse_list_scroll_whole_page = yes
colors_enabled = "yes"
{% endraw %}
{% endhighlight %}

{% highlight bash %}
systemctl --user enable mpd.service
{% endhighlight %}
