
Debian
====================
This directory contains files used to package britishpoundd/britishpound-qt
for Debian-based Linux systems. If you compile britishpoundd/britishpound-qt yourself, there are some useful files here.

## britishpound: URI support ##


britishpound-qt.desktop  (Gnome / Open Desktop)
To install:

	sudo desktop-file-install britishpound-qt.desktop
	sudo update-desktop-database

If you build yourself, you will either need to modify the paths in
the .desktop file or copy or symlink your britishpoundqt binary to `/usr/bin`
and the `../../share/pixmaps/britishpound128.png` to `/usr/share/pixmaps`

britishpound-qt.protocol (KDE)

