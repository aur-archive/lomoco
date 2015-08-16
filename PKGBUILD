# Maintainer: Jeff Mickey <j@codemac.net>
# Contributor: Shadowhand <woody.gilk@gmail.com>

pkgname=lomoco
pkgver=1.0
pkgrel=6
url="http://www.lomoco.org/"
pkgdesc="Logitech USB mouse configuration program"
license=('GPL')
depends=('libusb')
replaces=('lmctl')
arch=('i686' 'x86_64')
source=(http://www.lomoco.org/${pkgname}-${pkgver}.tar.gz
        lomoco_mouse.conf
        lomoco.sh)
md5sums=('f5197d0a3ee81229c3eecc1e03f7b08d'
         '182b10a7e4a1828a93c1d55ef7f81b97'
         'bc92f661641265b33b27895ef24028fd')
options=(!libtool)
backup=(etc/udev/lomoco_mouse.conf)


build() {
  cd ${srcdir}/${pkgname}-${pkgver}
  ./autogen.sh --prefix=/usr --mandir=/usr/share/man
  make
  make udev-rules
  make DESTDIR=${pkgdir} install
  
  # Fix and install udev rules and helpers
  sed -i 's|/etc/sysconfig/logitech_mouse|/etc/udev/lomoco_mouse.conf|g' udev/udev.lomoco
  sed -i 's|RUN="lomoco"|RUN+="lomoco.sh"|g' udev/lomoco.rules
  sed -i 's|SYSFS|ATTR|' udev/lomoco.rules
  install -D -m 644 udev/lomoco.rules ${pkgdir}/etc/udev/rules.d/80-lomoco.rules
  install -D -m 755 ../lomoco.sh ${pkgdir}/lib/udev/lomoco.sh
  install -D -m 644 ../lomoco_mouse.conf ${pkgdir}/etc/udev/
}
