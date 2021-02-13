---
layout: post
title: my dot xresources
categories: [setup]
tags: [urxvt, xresources, setup]
fullview: true
---

catatan .Xresources 

{% highlight bash %}
! ██╗░░██╗██████╗░███████╗███████╗░██████╗░██╗░░░██╗██████╗░░██████╗███████╗███████╗
! ╚██╗██╔╝██╔══██╗██╔════╝██╔════╝██╔═══██╗██║░░░██║██╔══██╗██╔════╝██╔════╝██╔════╝
! ░╚███╔╝░██████╔╝█████╗░░███████╗██║░░░██║██║░░░██║██████╔╝██║░░░░░█████╗░░███████╗
! ░██╔██╗░██╔══██╗██╔══╝░░╚════██║██║░░░██║██║░░░██║██╔══██╗██║░░░░░██╔══╝░░╚════██║
! ██╔╝░██╗██║░░██║███████╗███████║╚██████╔╝╚██████╔╝██║░░██║╚██████╗███████╗███████║
! ╚═╝░░╚═╝╚═╝░░╚═╝╚══════╝╚══════╝░╚═════╝░░╚═════╝░╚═╝░░╚═╝░╚═════╝╚══════╝╚══════╝
!
! -----------------------------------

Xft.dpi:			96
Xft.antialias:			true
Xft.rgba:			rgb
Xft.hinting:			true
Xft.hintstyle:			hintslight
Xft.autohint:			false
Xft.lcdfilter:			lcddefault

URxvt*perl-ext-common:		default,clipboard,keyboard-select,vtwheel,selection-to-clipboard,pasta
URxvt*clipboard.autocopy:	true
URxvt*keysym.C-C:		perl:clipboard:copy
URxvt*keysym.C-V:		perl:clipboard:paste
URxvt*keysym.C-A-V:		perl:clipboard:paste_escaped
URxvt.keysym.Control-Shift-V:   perl:pasta:paste
URxvt*url-select.underline:	false
URxvt*keysym.M-u:		perl:url-select:select_next
URxvt*keysym.M-Escape:		perl:keyboard-select:activate
URxvt*keysym.M-s:		perl:keyboard-select:search

URxvt*print-pipe:		"cat > /dev/null"
URxvt*termName:			xterm-256color
URxvt*iconFile:			/usr/share/icons/Paper/scalable/apps/utilities-terminal-symbolic.svg
URxvt*scrollstyle:		rxvt
URxvt*scrollBar:		false
URxvt*scrollTtyOutput:		false
URxvt*scrollWithBuffer:		true
URxvt*scrollTtyKeypress:	true
URxvt*secondaryScreen:		1
URxvt*secondaryScroll:		0
Xcursor*theme:			Paper
Xcursor*size:			16
URxvt*cursorUnderline:		true
URxvt*cursorBlink:		on
URxvt*pointerBlank:		false
URxvt*highlightSelection:	true
URxvt*lineSpace:		-1
URxvt*letterSpace:		-1
URxvt*depth:			32
URxvt*geometry:			480x280
URxvt*fading:			0
URxvt*saveLines:		9000
URxvt*loginShell:		true
URxvt*iso14755:			false
URxvt*iso14755_52:		false
URxvt*transparent:		true
URxvt*dynamicColors:		on
URxvt*allow_bold:		true
URxvt*boldMode:			on
URxvt*colorMode:		on
URxvt*colorBDMode:		on
URxvt*colorULMode:		on
URxvt*inheritPixmap:		true
URxvt*shading:			30
URxvt*blurRadius:		15
URxvt*font:			xft:MesloLGL Nerd Font:pixelsize=13
URxvt*boldFont:			xft:MesloLGS Nerd Font:style=Bold:pixelsize=13
URxvt*italicFont:		xft:MesloLGSDZ Nerd Font:style=Italic:pixelsize=13
URxvt*boldItalicFont :		xft:MesloLGLDZ Nerd Font Mono:style=Bold Italic:pixelsize=13
URxvt*colorIT:			#f92672
URxvt*colorBD:			#ff0000
URxvt*colorUL:			#f92672

*background:			#696ebf
*foreground:			#FDFDFD
!!*fading:			40
*fadeColor:			#002b36
*cursorColor:			#fdfdfd
*pointerColorBackground:	#586e75
*pointerColorForeground:	#93a1a1

#define base00 #272822
#define base01 #383830
#define base02 #49483e
#define base03 #75715e
#define base04 #a59f85
#define base05 #f8f8f2
#define base06 #f5f4f1
#define base07 #f9f8f5
#define base08 #ff0000
#define base09 #fd971f
#define base0A #f4bf75
#define base0B #a6e22e
#define base0C #3ae800
#define base0D #3ae800
#define base0E #ae81ff
#define base0F #cc6633

*.color0:       base00
*.color1:       base08
*.color2:       base0B
*.color3:       base0A
*.color4:       base0D
*.color5:       base0E
*.color6:       base0C
*.color7:       base05
*.color8:       base03
*.color9:       base08
*.color10:      base0B
*.color11:      base0A
*.color12:      base0D
*.color13:      base0E
*.color14:      base0C
*.color15:      base07

*.color16:      base09
*.color17:      base0F
*.color18:      base01
*.color19:      base02
*.color20:      base04
*.color21:      base06
{% endhighlight %}

{% highlight bash %}
xrdb ~/.Xresources
{% endhighlight %}
