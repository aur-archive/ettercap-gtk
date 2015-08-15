# $Id: PKGBUILD 103538 2010-12-21 10:37:25Z andrea $
# Maintainer: Hugo Doria <hugo@archlinux.org>
# Contributor: Tom Newsom <Jeepster@gmx.co.uk>

pkgname=ettercap-gtk
pkgver=NG_0.7.3
_origname=ettercap
_origver=NG-0.7.3
pkgrel=8
pkgdesc="A network sniffer/interceptor/logger for ethernet LANs - GTK"
arch=('i686' 'x86_64')
url="http://ettercap.sourceforge.net/"
license=('GPL')
depends=('ettercap' 'gtk2' 'libtool')
makedepends=('libnet')
options=('!libtool')
source=(http://downloads.sourceforge.net/${_origname}/${_origname}-${_origver}.tar.gz 
        'ettercap.desktop'
        'fix-segmentation-fault.patch')
md5sums=('28fb15cd024162c55249888fe1b97820'
        '6ef18fdd114297d4ed9e5104d309f071'
        'e9cc99f13fd23edaba6cddffc4d0ef34')

build() {
  cd ${srcdir}/${_origname}-${_origver}
  unset LDFLAGS

  # FS#21628
  patch -Np1 -i ${srcdir}/fix-segmentation-fault.patch

  libtoolize --force --copy
  aclocal
  autoconf
  ./configure --prefix=/usr --sysconfdir=/etc --enable-plugins
  sed -i 's/LTDL_SHLIB_EXT/\".so\"/' src/ec_plugins.c
  make
}

package() {
  install -Dm755 ${srcdir}/${_origname}-${_origver}/src/ettercap \
    ${pkgdir}/usr/bin/ettercap-gtk
  install -Dm644 ${srcdir}/ettercap.desktop \
    ${pkgdir}/usr/share/applications/ettercap.desktop
}
