# Maintainer: Benjamin Hedrich <kiwisauce (a) pagenotfound (dot) de>
# Based on package hts-tvheadend-svn by azleifel <azleifel at googlemail dot com>

pkgname=tvheadend-git
_gitname='tvheadend'
#_gitbranch='release/3.4'
_gitbranch=master
pkgver=3.5.243~g2b64995
pkgrel=1
pkgdesc="TV streaming server for Linux"
arch=('i686' 'x86_64')
url="http://www.lonelycoder.com/hts/tvheadend_overview.html"
license=('GPL3')
depends=('avahi' 'openssl' 'python2')
makedepends=('git')
optdepends=('xmltv: For an alternative source of programme listings')
provides=('tvheadend')
conflicts=('tvheadend' 'hts-tvheadend' 'hts-tvheadend-svn')
install=tvheadend.install

source=("$_gitname::git://github.com/tvheadend/tvheadend.git#branch=$_gitbranch"
    'tvheadend.install'
    'tvheadend.service')

md5sums=('SKIP'
    'bc6a5eb22716644d2ce3b4eac07bb735'
    '28dad6289dbe95961d2904fc77194ba5')

build() {

    cd ${srcdir}/${_gitname}
    msg " Starting configure..."
    ./configure --prefix=/usr --cpu="$ARCH" --mandir=/usr/share/man/man1 --python=python2 --release

    msg "Starting make..."
    make
}

package() {
    cd "$srcdir/$_gitname"
    make DESTDIR="$pkgdir/" install
    install -D -m 644 "$srcdir/tvheadend.service" "$pkgdir/etc/systemd/system/tvheadend.service"
}

pkgver() {
    cd "$srcdir/$_gitname"
    git describe --always | sed -e 's|patch|p|' -e 's|^v||' -e 's|-|.|' -e 's|-|~|'
}
