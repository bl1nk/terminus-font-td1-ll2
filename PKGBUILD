# $Id: PKGBUILD 101994 2013-12-03 15:26:54Z arodseth $
# Maintainer: Vesa Kaihlavirta <vegai@iki.fi>
# Maintainer: Alexander Rødseth <rodseth@gmail.com>
# Contributor: Kristoffer Fossgård <kfs1@online.no>
# Contributor: clonejo <clonejo@shakik.de>
# Contributor: Markus Cisler <m@kuchen.io>

_pkgname=terminus-font
pkgname=${_pkgname}-td1-ll2
pkgver=4.38
pkgrel=3
pkgdesc='Superb, monospace bitmap font (for X11 and console), with td1 and ll2 patches'
arch=('any')
url='http://sourceforge.net/projects/terminus-font/'
license=('GPL2' 'custom:OFL')
makedepends=('xorg-bdftopcf' 'fontconfig' 'xorg-mkfontscale' 'xorg-mkfontdir')
optdepends=('xorg-fonts-encodings' 'xorg-fonts-alias' 'xorg-font-utils' 'fontconfig')
conflicts=(terminus-font)
provides=(terminus-font)
install='terminus-font.install'
source=("http://downloads.sourceforge.net/project/$_pkgname/$_pkgname-$pkgver/$_pkgname-$pkgver.tar.gz")
sha256sums=('f6f4876a4dabe6a37c270c20bb9e141e38fb50e0bba200e1b9d0470e5eed97b7')

prepare() {
  chmod +x "$srcdir/$_pkgname-$pkgver/configure"
}

build() { 
  cd "$srcdir/$_pkgname-$pkgver"

  patch < alt/ll2.diff
  patch < alt/td1.diff

  ./configure --prefix=/usr \
    --x11dir=/usr/share/fonts/local \
    --psfdir=/usr/share/kbd/consolefonts
  make
}

package() {
  make -C "$_pkgname-$pkgver" DESTDIR="$pkgdir" install
  install -Dm644 "$srcdir/$_pkgname-$pkgver/75-yes-terminus.conf" \
    "$pkgdir/etc/fonts/conf.avail/75-yes-terminus.conf"
  install -Dm644 "$srcdir/$_pkgname-$pkgver/OFL.TXT" \
    "$pkgdir/usr/share/licenses/$_pkgname/LICENSE"
}

# vim:set ts=2 sw=2 et: