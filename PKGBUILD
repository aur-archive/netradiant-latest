# Mantainer: Artem Galichkin <doomer3dl at gmail dot com>
# Contributor: epsy < epsy46 at free dot fr >

pkgname=netradiant-latest
pkgver=20150214
pkgrel=1
pkgdesc="The bleeding edge version of the Q3A level map editor"
#url="http://icculus.org/netradiant/"
url="http://dev.xonotic.org/projects/xonotic/wiki/Netradiant"
arch=('i686' 'x86_64')
license=('GPL')
depends=('gtk2' 'gtkglext' 'libxml2' 'zlib' 'libpng')
makedepends=('git' 'subversion')
provides=('netradiant')
conflicts=('netradiant-svn-unfree' 'netradiant-svn' 'netradiant-bin32')

source=(http://epsy46.free.fr/code/netradiant/q3map2.sh)
md5sums=('fef4f71202db352395d68dabcbc9499a')

_gitroot="git://git.xonotic.org/xonotic/netradiant.git"
_gitname="netradiant"

build() {
    cd ${srcdir}

    if [ -d ${srcdir}/$_gitname ]; then
        (cd ${srcdir}/$_gitname && git pull origin)
    else
        git clone $_gitroot
    fi

    msg "git checkout done or server timeout"

    msg "Starting make..."

    cp -r ${srcdir}/$_gitname ${srcdir}/$_gitname-build
    cd ${srcdir}/$_gitname-build

    make || return 1
}

package() {
    mkdir -p ${pkgdir}/opt/
    mkdir -p ${pkgdir}/usr/bin/

    cd ${srcdir}/$_gitname-build
    
    cp -TR install ${pkgdir}/opt/netradiant/
    cp $srcdir/q3map2.sh ${pkgdir}/usr/bin/q3map2
    chmod +x ${pkgdir}/usr/bin/q3map2

    rm -rf ${srcdir}/$_gitname-build
}
