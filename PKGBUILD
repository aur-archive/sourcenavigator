# Contributor: Gustavo A. Gomez Farhat <gustavo_dot_gomez_dot_farhat at gmail_dot_com>
pkgname=sourcenavigator
pkgver=NG4.5
pkgrel=3
pkgdesc="A source code analysis tool"
arch=('i686' 'x86_64')
url="http://developer.berlios.de/projects/sourcenav"
license=('GPL2')
depends=('libx11')
source=(http://download.berlios.de/sourcenav/sourcenavigator-$pkgver.tar.bz2
  sourcenavigator.profile)
md5sums=('2be76f1e35b1b55630db9c8603473382'
         'a344c2b9c659a371b44b7e9de6254a76')

build() {
  export MAKEFLAGS="-j1"

  cd ${srcdir}/${pkgname}-${pkgver}
  ./configure --prefix=/opt/${pkgname}

  # fixes "Can't find a usable tk.tcl in the following directories" error
  sed -i '178,185 d' tk/library/listbox.tcl
  sed -i '453,460 d' tk/library/text.tcl

  make || return 1
  make DESTDIR=${pkgdir} install
  rm -rf ${pkgdir}/opt/${pkgname}/html
  install -m 755 -D ${srcdir}/sourcenavigator.profile ${pkgdir}/etc/profile.d/sourcenavigator.sh
}
