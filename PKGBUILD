# Maintainer: Georg Wagner <puxplaying_at_gmail_dot_com>

# Archlinux credits:
# Maintainer: Jan Alexander Steffens (heftig) <heftig@archlinux.org>
# Contributor: Jan de Groot <jgc@archlinux.org>

# Ubuntu credits:
# Robert Ancell: <https://salsa.debian.org/gnome-team/gnome-control-center>
# Marco Trevisan: <https://salsa.debian.org/gnome-team/mutter/-/blob/ubuntu/master/debian/patches/x11-Add-support-for-fractional-scaling-using-Randr.patch>

pkgname=gnome-control-center-x11-scaling
_pkgname=gnome-control-center
pkgver=43.2
pkgrel=1
pkgdesc="GNOME's main interface to configure various aspects of the desktop with X11 fractional scaling patch"
url="https://gitlab.gnome.org/GNOME/gnome-control-center"
license=(GPL3)
arch=(x86_64)
depends=(accountsservice cups-pk-helper gnome-bluetooth-3.0 gnome-desktop-4
         gnome-online-accounts gnome-settings-daemon gsettings-desktop-schemas
         gtk4 libgtop libnma-gtk4 sound-theme-freedesktop upower libpwquality
         gnome-color-manager smbclient libmm-glib libgnomekbd libibus libgudev
         bolt udisks2 libadwaita gsound colord-gtk4 gcr libmalcontent)
makedepends=(docbook-xsl modemmanager git python meson)
checkdepends=(python-dbusmock python-gobject xorg-server-xvfb)
conflicts=($_pkgname)
provides=($_pkgname)
optdepends=('system-config-printer: Printer settings'
            'gnome-user-share: WebDAV file sharing'
            'gnome-remote-desktop: screen sharing'
            'rygel: media sharing'
            'openssh: remote login'
            'power-profiles-daemon: Power profiles support'
            'malcontent: application permission control')
groups=(gnome)
_commit=ec6ea052669784800846a1429dbaf3137a4b87dd  # tags/43.2^0
source=("git+https://gitlab.gnome.org/GNOME/gnome-control-center.git#commit=$_commit"
        "git+https://gitlab.gnome.org/GNOME/libgnome-volume-control.git"
        "display-Allow-fractional-scaling-to-be-enabled.patch::https://salsa.debian.org/gnome-team/gnome-control-center/-/raw/055a7c0cb66a8de56e2ec6564f2cf9f3f61e705b/debian/patches/ubuntu/display-Allow-fractional-scaling-to-be-enabled.patch"
        "display-Support-UI-scaled-logical-monitor-mode.patch::https://salsa.debian.org/gnome-team/gnome-control-center/-/raw/055a7c0cb66a8de56e2ec6564f2cf9f3f61e705b/debian/patches/ubuntu/display-Support-UI-scaled-logical-monitor-mode.patch"
  	pixmaps-dir.diff)
sha256sums=('SKIP'
            'SKIP'
            '354e9d6fa7d4caa560d348a1c75337a09d80f1434f4ddf3f693d4ce2a3408163'
            'fe7868d62177643d0d493ec121bb6cc15c0cbe7a4058ac097546a245c4344b5d'
            '4c6205010376fdaafdd672c7fc6a1eea3beaa19d18fbccb3fdba2d2ca24aed7d')

pkgver() {
  cd $_pkgname
  git describe --tags | sed 's/[^-]*-g/r&/;s/-/+/g'
}

prepare() {
  cd $_pkgname

  # Install bare logos into pixmaps, not icons
  git apply -3 ../pixmaps-dir.diff

  git submodule init subprojects/gvc
  git submodule set-url subprojects/gvc "$srcdir/libgnome-volume-control"
  git -c protocol.file.allow=always submodule update

  # Support UI scaled logical monitor mode (Marco Trevisan, Robert Ancell)
  patch -p1 -i "${srcdir}/display-Support-UI-scaled-logical-monitor-mode.patch"
  patch -p1 -i "${srcdir}/display-Allow-fractional-scaling-to-be-enabled.patch"
}

build() {
  local meson_options=(
    -D documentation=true
    -D malcontent=true
  )

  arch-meson $_pkgname build "${meson_options[@]}"
  meson compile -C build
}

check() {
  GTK_A11Y=none meson test -C build --print-errorlogs
}

package() {
  meson install -C build --destdir "$pkgdir"
  install -d -o root -g 102 -m 750 "$pkgdir/usr/share/polkit-1/rules.d"
}
