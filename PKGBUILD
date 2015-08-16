# Maintainer: Christoph Vigano <mail at cvigano dot de>
# Contributor: Biru Ionut <ionut@archlinux.ro>
# Contributor: Pierre Schmitz <pierre@archlinux.de>
# Contributor: Mikko Seppälä <t-r-a-y@mbnet.fi>
_pkgbasename=gnutls
pkgname=lib32-$_pkgbasename
pkgver=3.0.11
pkgrel=1
pkgdesc="A library which provides a secure layer over a reliable transport layer (32-bit)"
arch=('x86_64')
license=('GPL3' 'LGPL')
url="http://www.gnu.org/software/gnutls/"
options=('!libtool')
depends=('lib32-zlib' 'lib32-nettle>=2.4' 'lib32-p11-kit')
makedepends=('gcc-multilib' 'lib32-libidn')
source=(ftp://ftp.gnu.org/gnu/gnutls/${_pkgbasename}-${pkgver}.tar.xz)
md5sums=('ca3370b39f7910538a0d6c02bec7a142')

build() {
  export CC="gcc -m32"
  export CXX="g++ -m32"
  export PKG_CONFIG_PATH="/usr/lib32/pkgconfig"

  cd ${srcdir}/${_pkgbasename}-${pkgver}

  # build fails without --disable-hardware-acceleration because of assembler errors
  ./configure --prefix=/usr --libdir=/usr/lib32 \
    --with-zlib \
    --disable-static \
    --disable-guile \
    --disable-valgrind-tests --disable-hardware-acceleration
  make
}

package() {
  cd "${srcdir}/${_pkgbasename}-${pkgver}"
  make DESTDIR="${pkgdir}" install
  find $pkgdir

  rm -rf "${pkgdir}"/usr/{bin,include,share}
}
