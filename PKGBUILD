# Maintainer: Charles Bos <charlesbos1 AT gmail>
# Contributor: Xiao-Long Chen <chenxiaolong@cxl.epac.to>
# Contributor: Jan Alexander Steffens (heftig) <jan.steffens@gmail.com>
# Contributor: Andrea Scarpino <andrea@archlinux.org>
# Contributor: György Balló <ballogy@freestart.hu>

pkgname=zeitgeist-ubuntu
pkgver=0.9.14
_ubuntu_rel=0ubuntu4
pkgrel=1
pkgdesc="Service logging user activities and events"
arch=('i686' 'x86_64')
url="http://zeitgeist-project.com/"
license=('GPL2' 'LGPL2.1')
depends=('json-glib' 'telepathy-glib' 'gtk3')
makedepends=('intltool' 'gobject-introspection' 'vala' 'raptor' 'python2-rdflib')
provides=('zeitgeist-datahub' "zeitgeist=${pkgver}")
conflicts=('zeitgeist-datahub' 'zeitgeist')
replaces=('zeitgeist-datahub')
source=("https://launchpad.net/zeitgeist/${pkgver%.*}/${pkgver}/+download/zeitgeist-${pkgver}.tar.xz"
        "https://launchpad.net/ubuntu/+archive/primary/+files/zeitgeist_${pkgver}-${_ubuntu_rel}.debian.tar.gz")
sha512sums=('9886396ea153fc12de81fdee2acf645b33a2af0c0fa3533c18f6c80c68c506ee9f790f37f99677ce6c3546a0f9ef5e5c251bc9411e0d882df796479edd9e817c'
            'b0f482f11403f9afdbfbd3419ecb41773167636419883986e8eaa3db6035bcc1cdfb579132c9cad516d956ed3f8110e07523c380274136eccb25ed6a38caee0f')

prepare() {
  cd "${srcdir}/zeitgeist-${pkgver}"
  sed -i 's/python -/$PYTHON -/' configure configure.ac
  patch -p1 -i "${srcdir}/debian/patches/pre_populator.patch"
}

build() {
  cd "${srcdir}/zeitgeist-${pkgver}"
  export PYTHON=/usr/bin/python2
  autoreconf -vfi
  ./configure \
    --prefix=/usr \
    --sysconfdir=/etc \
    --localstatedir=/var \
    --libexecdir=/usr/lib/zeitgeist
  make
}

package() {
  cd "${srcdir}/zeitgeist-${pkgver}"
  make DESTDIR="${pkgdir}" install
}
