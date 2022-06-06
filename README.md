# gnome-control-center-x11-scaling

gnome-control-center build with Ubuntu patches for Xorg fractional scaling on Manjaro / Arch Linux.

This package requires [mutter-x11-scaling](https://github.com/puxplaying/mutter-x11-scaling) to work.

Applied patches are for proper multi-monitor management and a toggle to enable/disable fractional scaling. [[1]](https://salsa.debian.org/gnome-team/gnome-control-center/-/blob/ubuntu/master/debian/patches/ubuntu/display-Support-UI-scaled-logical-monitor-mode.patch) [[2]](https://salsa.debian.org/gnome-team/gnome-control-center/-/blob/ubuntu/master/debian/patches/ubuntu/display-Allow-fractional-scaling-to-be-enabled.patch)

All credits belong to [Arch Linux](https://www.archlinux.org/packages/extra/x86_64/mutter/) and [Ubuntu](https://salsa.debian.org/gnome-team/gnome-control-center/-/tree/ubuntu/master/debian/patches), this package is available on [Manjaro](https://manjaro.org/) and the [AUR](https://aur.archlinux.org/packages/gnome-control-center-x11-scaling).

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
