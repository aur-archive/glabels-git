# Contributor: Dmitry Korzhevin <dkorzhevin at lsupport dot net>
# Maintainer: Mario Blättermann <mariobl@gnome.org>
 
pkgname=glabels-git
pkgver=20150120
pkgrel=1
pkgdesc="Creating labels and business cards the very easy way"
arch=('i686' 'x86_64')
license=('GPL' 'LGPL')
url="http://glabels.sourceforge.net/"
depends=('gtk3>=2.91.7' 'dconf' 'gnome-common>=3' 'desktop-file-utils' 'shared-mime-info' 'evolution-data-server' 'zint>=2.4.0' 'yelp-tools')
conflicts=(glabels-unstable glabels)
provides=(glabels)
makedepends=('pkgconfig' 'gnome-doc-utils' 'intltool')
options=('!libtool')
_gitroot="git://git.gnome.org/glabels"
_gitname="glabels"
install=glabels.install
source=()
md5sums=()

pkgver() {
  cd "${srcdir}/${_gitname}"
  #date +"%Y%m%d"
  #git log -1 --format="%cd.g%h" --date=short | sed 's/-/./g' 
  git log -1 --format="%cd" --date=short | sed 's|-||g'
  #echo "$(git log -1 --format="%cd" --date=short | sed 's|-||g').$(git rev-list --count master)"
}

build() {
  cd ${srcdir}
  msg "Connecting to GNOME GIT server...."

  if [ -d ${srcdir}/$_gitname ] ; then
          cd $_gitname && git pull origin
          msg "The local files are updated."
  else
          git clone $_gitroot
  fi

  cd ${srcdir}/$_gitname
  ./autogen.sh --prefix=/usr
  make
}
package() {
  cd ${srcdir}/$_gitname
  make DESTDIR=$pkgdir install

  mkdir -p $startdir/pkg/usr/share/glib-2.0/schemas
  install -c -m 644 ${srcdir}/$_gitname/data/schemas/org.gnome.glabels-3.gschema.xml \
	"$startdir/pkg/usr/share/glib-2.0/schemas"
}
