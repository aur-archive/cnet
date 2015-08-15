# Maintainer: Jake Tucker <jaketckr+arch@gmail.com>

pkgname=cnet
pkgver=3.3.1
pkgrel=3
pkgdesc="Enables development of / experimentation with a variety of protocols in networks"
arch=('i686' 'x86_64')
url="http://www.csse.uwa.edu.au/cnet/"
license=('GPL2')
depends=('tk>=8.4' 'elfutils')
options=('staticlibs')
install="cnet.install"
source=(Makefile.patch
        src.Makefile.linux.patch
        support.Makefile.common.patch
        cnet.sh)
md5sums=('c24a6296f95fdd02121cce557949eaee'
         '0b70b1ad53ed27a5aec71f2dc93d7125'
         '76282da17f289352657ab0dd927b9167'
         'd1c2b8e09ee6b2a811ed79505dce6c70')

pkgver() {
  curl --data "email=&role=other&role-other=&location=&country=&os=linux&os-other=" \
      https://secure.csse.uwa.edu.au/run/cnet-download > $srcdir/$pkgname.tgz
  tar -xf $srcdir/$pkgname.tgz
  grep -E "VERSION[ ]*" $srcdir/$pkgname*/Makefile | grep -oEi "[0-9]+(.[0-9])*"
}

prepare() {
  patch "$pkgname-$pkgver/src/Makefile.linux" < src.Makefile.linux.patch
  patch "$pkgname-$pkgver/support/Makefile.common" < support.Makefile.common.patch
  patch "$pkgname-$pkgver/Makefile" < Makefile.patch
}

build() {
  cd "$srcdir/$pkgname-$pkgver"
  make PREFIX=$pkgdir/usr
}

package() {
  cd "$srcdir/$pkgname-$pkgver"
  make PREFIX=$pkgdir/usr install
  mkdir -p $pkgdir/etc/profile.d
  cp $srcdir/cnet.sh $pkgdir/etc/profile.d/cnet.sh
}
