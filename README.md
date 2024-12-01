# jokertracer1488

A Cisco Packet Tracer 8.0.1 version pacman package for CFUV opensource people.

## Installation

#### **The way it should've been**:

##### ATTENTION: THIS METHOD OF INSTALL IS PURE PROFANITY AND ALSO DEPRECATED (I don't have a clue about the containments of the .pkg archive)

Also will leave these changes to for them to be in repo history lol

**Appropriate** method of cloning this repo (with all the git lfs limited stuff)

```bash
git clone <URL>
cd /path/to/repo
git lfs install
git lfs pull
```
(any other **method** will cause corrupt or wrong sha512sum of large files)

And after you **build your own pacman package** follow these steps:

 - On .pkg.tar.zst run command:

   `sudo pacman -U packagename-packageversion-arch.pkg.tar.zst`

 -  - To uninstall this package just do a normal pacman uninstall command (e.g. `sudo pacman -Rcns packagename`)


## **BUILD FROM SOURCE** (**ONLY** option)

Wayland users *(and others)* can download source repo and build with `makepkg -si` - [the source repo (packettracer folder)](https://github.com/kenctxncy/cisco-packet-tracer-801)

**Important:** you need to use **the same method** as was described above, because large files will be broken and have wrong checksums.

**If you experience checksum validation troubles** you can simply ignore them with a flag or create an issue idk

#### **The way it turned out**:

Due to (((Git LFS data quota issue))), download from these repositories is ~~possible only few times a month~~ problematic. 

Right now I'm looking for workarounds, stay tuned.

**UPD:** Still looking for workarounds, but who cares if you can find all the stuff (.deb package to build from source) on archive.org or whatever


## Known issues:

If you're a **KDE Plasma user** you may be missing some icons ~~(but who cares if you're starting packettracer from terminal)~~

Didn't happen to me but the following commands might fix this issue:

```bash
sudo mkdir -p "${pkgdir}/usr/share/icons/hicolor/48x48/mimetypes"
sudo mv "${pkgdir}/usr/share/icons/gnome/48x48/mimetypes/pka.png" "${pkgdir}/usr/share/icons/hicolor/48x48/mimetypes/application-x-pka.png"
sudo mv "${pkgdir}/usr/share/icons/gnome/48x48/mimetypes/pks.png" "${pkgdir}/usr/share/icons/hicolor/48x48/mimetypes/application-x-pks.png"
sudo mv "${pkgdir}/usr/share/icons/gnome/48x48/mimetypes/pksz.png" "${pkgdir}/usr/share/icons/hicolor/48x48/mimetypes/application-x-pksz.png"
sudo mv "${pkgdir}/usr/share/icons/gnome/48x48/mimetypes/pkt.png" "${pkgdir}/usr/share/icons/hicolor/48x48/mimetypes/application-x-pkt.png"
sudo mv "${pkgdir}/usr/share/icons/gnome/48x48/mimetypes/pkz.png" "${pkgdir}/usr/share/icons/hicolor/48x48/mimetypes/application-x-pkz.png"
sudo rmdir -p "${pkgdir}/usr/share/icons/gnome/48x48/mimetypes"
```

### **Wayland session issues**

If you're running X11 everything should work smoothly.

But, as always, wayland users need to adapt (especially for legacy packages such as this version of packettracer).

So after setting `export QT_QPA_PLATFORM=xcb` packettracer ***will start*** and 

`/usr/bin/packettracer: line 8:  3441 Aborted     (core dumped) ./PacketTracer "$@" > /dev/null 2>&1`

error will begone *(if you still can't use packettracer try running it with* `--no-sandbox` *flag*).

You can also add exec command to your \*.desktop files when building from source *(provided .pkg file isn't tuned for your system, so for a "perfect install" you should download the source folder, build and automate the envvars by yourself (gl with [archwiki.org](https://archwiki.org)).
So the .desktop files will be in your PKGBUILD folder, e.g.* `~/Downloads/cisco-packet-tracer-801/...` *)*:

Edit the following lines:

 - in cisco-pt.desktop and cisco-ptsa.desktop:
   `Exec=env QT_QPA_PLATFORM=xcb /opt/packettracer/packettracer %f`

### **Application interface is a mess**

Happened to me on KDE Plasma. This issue is caused by gnome, which is native for the .deb package we're building from. If that didnt work, then it may also be a mismatch of application's gtk theme (which is configured in ~/.config/gtkrc file) and your selected desktop theme. To fix this you need to again set your env vars when starting from terminal or edit your \*.desktop files in PKGBUILD folder:

First, try:

 - `env XDG_CURRENT_DESKTOP=GNOME packettracer`

if it worked, you may add this variable in your .desktop `Exec=...` line.

**If it didn't**, then try setting a light theme variation of your current one. In case of KDE, it was setting a QT theme:

 - `env XDG_CURRENT_DESKTOP=GNOME QT_QPA_PLATFORMTHEME=<YOURTHEME> (check yours in /usr/share/themes/...)`

**If it's still not working**, try setting gtk theme to default, by adding `GTK_THEME=Default` to your`env` terminal/Exec line

And you're done

### **Packet Tracer Activity docs won't render**

Discovered recently. This is a flaw in .deb ubuntu package. It's over. There is nothing we can do... Just install a fresh version in which HTML render isn't broken. Also try to run PT using wine ~~or even install windows~~
