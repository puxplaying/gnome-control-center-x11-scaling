# gnome-control-center-x11-scaling

# GNOME 42 is currently not supported! See also [here](https://github.com/puxplaying/gnome-control-center-x11-scaling/issues/3)
gnome-control-center build with Ubuntu patches for Xorg fractional scaling on Manjaro / Arch Linux 

All Credits belong to [Arch Linux](https://www.archlinux.org/packages/extra/x86_64/gnome-control-center/) and [Ubuntu](https://salsa.debian.org/gnome-team/gnome-control-center/-/tree/ubuntu/master/debian/patches)

---

Build instructions for Manjaro / Arch Linux:

```
sudo pacman -Syu base-devel git
git clone https://github.com/puxplaying/gnome-control-center-x11-scaling.git
cd gnome-control-center-x11-scaling
makepkg -srci
```

---

![1](https://user-images.githubusercontent.com/28549766/135753045-1296531d-8d06-45f3-af10-f8b8cdbee720.png)
