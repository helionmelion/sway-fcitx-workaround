### sway fcitx workaround ###

This is a simple workaround to use fcitx inside sway window manager (wayland).

the goal is to use fcitx-mozc (japanese input) within sway, sine actually it is buggy. Fcitx-mozc is pretty stable in i3-wm (X11).

Details of my home desktop:

- using Arch Linux
- using SDDM display manager
- sway windows manager
- zsh shell

Seems fcitx must be executed before sway.

SDDM will source .zprofile if it exists. 

So created a $home/.zprofile

	export XKB_DEFAULT_MODEL=jp106
	export XKB_DEFAULT_LAYOUT=jp,br
	export XKB_DEFAULT_OPTIONS=grp:rctrl_toggle
	export GTK_IM_MODULE=fcitx
	export QT_IM_MODULE=fcitx
	export XMODIFIERS=@im=fcitx
	fcitx -r

This will set variables and the last line will execute fcitx.

Must be noted that toggle key combinations here and fcitx must not be the same. So I choose rctrl here and ctrl+space in fcitx.

Inside sway, fcitx-configtool will not work. Launching another instance of fcitx will correct this.

Put inside ~/.config/sway/config

	exec fcitx -r

Maybe it is better to use fcitx -D to not run as daemon. Yet to be tested combinations in .zprofile and sway config to avoid multiple allocation of fcitx and dbus-daemon upon logoff/logon. 

Seems this workaround does not mess up with current fcitx i3-wm funcionality.

Good luck.
