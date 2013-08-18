# Maintainer: Benjamin Hedrich <kiwisauce (a) pagenotfound (dot) de>
# Based on package hts-tvheadend-svn by azleifel <azleifel at googlemail dot com>

pkgname=tvheadend-git
_gitname='tvheadend'
pkgver=20130422.v3.5_116_ga2ccbb2
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
backup=('etc/conf.d/tvheadend')
install=tvheadend.install

source=("$_gitname::git://github.com/tvheadend/tvheadend.git"
	'tvheadend.conf.d'
 	'tvheadend.rc.d' 
	'tvheadend.service')

md5sums=('SKIP'
         '854845963c364cdcefcbd473f713179b'
         'a8d7b66c6592aabde7556b253f5e0d54'
         'b546f4486f0d28bea13ad1fb676acb27')

build() {
    cd ${_gitname}
    msg "Creating build directory"
    cd ${srcdir}
    [ -d ${_gitname}-build ] && rm -rf ${_gitname}-build
    /usr/share/git/workdir/git-new-workdir ${_gitname} ${_gitname}-build master
    
    msg "Starting make..."
    cd ${_gitname}-build
    ./configure --prefix=/usr --mandir=/usr/share/man/man1 --python=python2 --release
    make
}

package() {
    cd "$srcdir/$_gitname-build"

    make DESTDIR="$pkgdir/" install

    install -D -m 755 "$srcdir/tvheadend.rc.d" "$pkgdir/etc/rc.d/tvheadend"
    install -D -m 644 "$srcdir/tvheadend.conf.d" "$pkgdir/etc/conf.d/tvheadend"
    install -D -m 644 "$srcdir/tvheadend.service" "$pkgdir/usr/lib/systemd/system/tvheadend.service"
}

pkgver() {
    cd "$srcdir/$_gitname"
    echo $(git log -1 --format="%ci" | sed 's/.*\([0-9]\{4\}\)-\([0-9]\{2\}\)-\([0-9]\{2\}\).*/\1\2\3/').$(git describe --always | tr '-' '_' )
}
