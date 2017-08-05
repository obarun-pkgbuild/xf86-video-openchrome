# Maintainer: Eric Vidal <eric@obarun.org>
# based on the original https://projects.archlinux.org/svntogit/packages.git/tree/trunk?h=packages/xf86-video-openchrome
# 						Maintainer: AndyRTR <andyrtr@archlinux.org>
# 						Contributor: Paul Mattal <paul@mattal.com>
# 						Contributor: Juergen Hoetzel <juergen@hoetzel.info>

pkgname=xf86-video-openchrome
#_commit=8c819ed # 7 digits # = 0.6.0 RC1
#pkgver=0.5.0+279+g8c819ed
pkgver=0.6.0
pkgrel=2
pkgdesc="X.Org Openchrome drivers"
arch=(x86_64)
license=('custom')
url="http://www.freedesktop.org/wiki/Openchrome/"
depends=('libdrm' 'libxvmc')
optdepends=('unichrome-dri')
makedepends=('xorg-server-devel' 'X-ABI-VIDEODRV_VERSION=23') # 'git')
conflicts=('xorg-server<1.19' 'X-ABI-VIDEODRV_VERSION<23' 'X-ABI-VIDEODRV_VERSION>=24'
           'xf86-video-via' 'xf86-video-unichrome' 'openchrome')
replaces=('openchrome' 'xf86-video-via')
groups=('xorg-drivers')
options=('!emptydirs')
source=(https://xorg.freedesktop.org/archive/individual/driver/${pkgname}-${pkgver}.tar.bz2)
source=("git://anongit.freedesktop.org/openchrome/xf86-video-openchrome#commit=${_commit}")
sha256sums=('SKIP')
validpgpkeys=('6DD4217456569BA711566AC7F06E8FDE7B45DAAC') # Eric Vidal

#pkgver() {
#  cd $pkgname
#  git describe --long | sed 's/-/+/g'
#  git describe --long | sed "s/openchrome-//;s/-/./g"
#  git describe --long | sed "s/openchrome-//;s/0.5/0.5.200/;s/-/+/g"
#  git describe --long | sed "s/openchrome-//;s/0.5/0.5.0/;s/-/+/g"
#}

prepare() {
  cd ${pkgname}
  NOCONFIGURE=1 ./autogen.sh
}


build() {
  cd ${pkgname} #-${pkgver}
  ./configure --prefix=/usr
  make
}

check() {
  cd ${pkgname} #-${pkgver}
  make check
}

package() {
  cd ${pkgname} #-${pkgver}
  make DESTDIR="${pkgdir}" install
  install -m755 -d "${pkgdir}/usr/share/licenses/${pkgname}"
  install -m644 COPYING "${pkgdir}/usr/share/licenses/${pkgname}/"
}