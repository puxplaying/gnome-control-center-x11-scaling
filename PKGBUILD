# Maintainer: puxplaying (Georg Wagner) <puxplaying@gmail.com>

# Archlinux credits:
# Maintainer: Jan Alexander Steffens (heftig) <heftig@archlinux.org>
# Contributor: Jan de Groot <jgc@archlinux.org>

# Ubuntu credits:
# Sebastien Bacher: <https://salsa.debian.org/gnome-team/gnome-control-center>
# Marco Trevisan: <https://salsa.debian.org/gnome-team/mutter/-/blob/ubuntu/master/debian/patches/x11-Add-support-for-fractional-scaling-using-Randr.patch>

pkgbase=gnome-control-center
pkgname=$pkgbase-x11-scaling
pkgver=3.38.2
pkgrel=1
pkgdesc="GNOME's main interface to configure various aspects of the desktop"
url="https://gitlab.gnome.org/GNOME/gnome-control-center"
license=(GPL2)
arch=(x86_64)
depends=(accountsservice cups-pk-helper gnome-bluetooth gnome-desktop
         gnome-online-accounts gnome-settings-daemon gsettings-desktop-schemas gtk3
         libgtop nm-connection-editor sound-theme-freedesktop upower libpwquality
         gnome-color-manager smbclient libmm-glib libgnomekbd grilo libibus
         cheese libgudev bolt udisks2 libhandy gsound colord-gtk)
makedepends=(docbook-xsl modemmanager git python meson)
checkdepends=(python-dbusmock python-gobject xorg-server-xvfb)
conflicts=($pkgbase)
provides=($pkgbase)
optdepends=('system-config-printer: Printer settings'
            'gnome-user-share: WebDAV file sharing'
            'gnome-remote-desktop: screen sharing'
            'rygel: media sharing'
            'openssh: remote login')
groups=(gnome)
_commit=0ae321b67d1c31d9bc209807aa6103d01a95e726  # tags/3.38.2^0
source=("git+https://gitlab.gnome.org/GNOME/gnome-control-center.git#commit=$_commit"
        "git+https://gitlab.gnome.org/GNOME/libgnome-volume-control.git"
        "0019-display-Support-UI-scaled-logical-monitor-mode.patch::https://salsa.debian.org/gnome-team/gnome-control-center/-/raw/ubuntu/master/debian/patches/0019-display-Support-UI-scaled-logical-monitor-mode.patch"
        "0024-display-Allow-fractional-scaling-to-be-enabled.patch::https://salsa.debian.org/gnome-team/gnome-control-center/-/raw/ubuntu/master/debian/patches/0024-display-Allow-fractional-scaling-to-be-enabled.patch")
sha256sums=('SKIP'
            'SKIP'
            '29be1d77bfc84b8cdea72df222b0ad1ce65a1452cdab7bec240cda7769ca05f5'
            'eb095fe779222e385e2cce0c2eb597c734b6d9c8446408bfdb6f07de367eb5e7')

pkgver() {
  cd $pkgbase
  git describe --tags | sed 's/^GNOME_CONTROL_CENTER_//;s/_/./g;s/-/+/g'
}

prepare() {
  cd $pkgbase
  git submodule init
  git submodule set-url subprojects/gvc "$srcdir/libgnome-volume-control"
  git submodule update
  
  # Ubuntu Patches for X11 fractional scaling
  patch -p1 -i "${srcdir}/0019-display-Support-UI-scaled-logical-monitor-mode.patch"
  patch -p1 -i "${srcdir}/0024-display-Allow-fractional-scaling-to-be-enabled.patch"
}


build() {
  arch-meson $pkgbase build -D documentation=true
  meson compile -C build
}

check() {
  meson test -C build --print-errorlogs
}

package() {
  DESTDIR="$pkgdir" meson install -C build
  install -d -o root -g 102 -m 750 "$pkgdir/usr/share/polkit-1/rules.d"
}

