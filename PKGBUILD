# Maintainer: Doug Newgard <scimmia22 at outlook dot com>
# Contributor: Andries Radu <admiral0@live.it>
# Contributor: Michele Gastaldo <pikiweb@gmail.com>
# Contributor: Changaco <changaco Î±Ï„ changaco Î´Î¿Ï„ net>

pkgname=python2-elementary-svn
pkgver=76576
pkgrel=3
pkgdesc="Python2 bindings for Elementary"
arch=('i686' 'x86_64')
url="http://www.enlightenment.org"
license=('LGPL3')
depends=('elementary-svn' 'python2-evas-svn')
makedepends=('subversion' 'cython2')
conflicts=('python2-elementary')
provides=('python2-elementary')
options=('!libtool' '!emptydirs')

_svntrunk="http://svn.enlightenment.org/svn/e/trunk/BINDINGS/python/python-elementary/"
_svnmod="python-elementary"

build() {
  cd "$srcdir"

  msg "Connecting to SVN server...."

  if [[ -d "$_svnmod/.svn" ]]; then
    (cd "$_svnmod" && svn up -r "$pkgver")
  else
    svn co "$_svntrunk" --config-dir ./ -r "$pkgver" "$_svnmod"
  fi

  msg "SVN checkout done or server timeout"
  msg "Starting build..."

  rm -rf "$srcdir/$_svnmod-build"
  svn export "$srcdir/$_svnmod" "$srcdir/$_svnmod-build"
  cd "$srcdir/$_svnmod-build"

  PYTHON=/usr/bin/python2 \
  ./autogen.sh --prefix=/usr

  make
}

package() {
  cd "$srcdir/$_svnmod-build"
  make DESTDIR="$pkgdir" install

  rm -r "$srcdir/$_svnmod-build"
}
