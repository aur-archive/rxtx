# $Id$
# Maintainer: Balló György <ballogyor+arch at gmail dot com>
# Contributor: Vitaliy Berdinskikh ur6lad[at]i.ua

pkgname=rxtx
pkgver=2.2pre2
pkgrel=7
pkgdesc="Java library for serial IO"
arch=('i686' 'x86_64')
url="http://rxtx.qbang.org/"
license=('LGPL')
depends=('glibc' 'java-runtime')
makedepends=('java-environment')
options=('!libtool')
install=$pkgname.install
source=(http://rxtx.qbang.org/pub/$pkgname/$pkgname-$pkgver.zip
        utsrelease.patch
        rxtx-2.2-lock.patch
        rxtx-2.2-fhs_lock.patch
        ttyACM_port.patch)
md5sums=('7eedb18e3f33a427e2b0e9be8ce3f94c'
         '2f21ec5eb108f871815242698b6150f1'
         '1f7c43d582bfe9daea22d7f7057436da'
         'f4d22d263f45cd1d4db6242dd0ac78ae'
         '903a3fe0067d0682dd5f64483c741df6')

build() {
  cd "$srcdir/$pkgname-$pkgver"

  # Fix build
  patch -Np1 -i "$srcdir/utsrelease.patch"

  # Fix lockdir patch
  patch -Np1 -i "$srcdir/rxtx-2.2-lock.patch"

  # Fix buffer overflow
  patch -Np1 -i "$srcdir/rxtx-2.2-fhs_lock.patch"

  # Enable more ports
  patch -Np1 -i "$srcdir/ttyACM_port.patch"

  ./configure --prefix=/usr --sysconfdir=/etc --localstatedir=/var \
              --disable-static
  make -j1
}

package() {
  cd "$srcdir/$pkgname-$pkgver"

  mkdir -p "$pkgdir"/usr/{lib,share/java/rxtx}
  make JHOME="$pkgdir/usr/share/java/rxtx" RXTX_PATH="$pkgdir/usr/lib" install
}
