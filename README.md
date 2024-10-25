# jokertracer1488

A Cisco Packet Tracer 8.0.1 version pacman package for CFUV opensource people

## Installation

Download .pkg.tar.zst pacman package and run command:

`sudo pacman -U  `***packagename***`-`***packageversion***`-`***arch***`.pkg.tar.zst`

To uninstall package just do a normal pacman uninstall command (e.g. `sudo pacman -Rcns  `***packagename***)


## Or you can **build from source**

If you're perfectionist you actually can - [the source repo (packettracer folder)](https://github.com/kenctxncy/cisco-packet-tracer-801)

## Known issues:

If you're a **KDE Plasma user** you may be missing some icons ~~(but who cares if you're starting it from terminal)~~

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

If you're running X11 everything should work smoothly

But, as always, wayland users need to adapt (especially for legacy packages such as this version of packettracer)

So after setting `export QT_QPA_PLATFORM=xcb` packettracer ***will start*** and `/usr/bin/packettracer: line 8:  3441 Aborted     (core dumped) ./PacketTracer "$@" > /dev/null 2>&1` error will begone *(if you still can't use packettracer try running it with* `--no-sandbox` *flag*)

You can also add exec command to your \*.desktop files *(provided .pkg file is not as* **beautiful** *as it can be, so for a "perfect install", if you want, you can download the source folder, build and automate the envvars by yourself (gl with [archwiki,org](https://archwiki.org)).
So the .desktop files will be in your PKGBUILD folder, e.g.* `~/Downloads/cisco-packet-tracer-801/...` *)*:

Edit the following lines:

 - in cisco-pt.desktop and cisco-ptsa.desktop:
   `Exec=env QT_QPA_PLATFORM=xcb /opt/packettracer/packettracer %f`

And you're done
