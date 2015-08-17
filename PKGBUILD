# Maintainer: Xtricman <xtricman@gmail.com>
pkgname=rhythmcat2-git
_pkgname=rhythmcat2
pkgver=20130331
pkgrel=1
pkgdesc="A music player which can be used under Linux"
arch=('i686' 'x86_64')
url="https://github.com/supercatexpert/RhythmCat2"
license=('GPL3')
depends=('gtk3'
         'gst-plugins-base'
         'gst-plugins-good'
         'gtk-doc'
         'python'
         'gobject-introspection'
         'hicolor-icon-theme'
         'desktop-file-utils')
makedepends=('git')
optdepends=('gst-plugins-bad: play restricted audio format' 
            'gst-plugins-ugly: play restricted audio format')
options=('!emptydirs' '!libtool')
source=(RhythmCat2.desktop)
md5sums=("7ee4cb341d3e5490b21fd40b2b801882")
_gitroot="https://github.com/supercatexpert/RhythmCat2.git"
_gitname=${_pkgname}
install=${_pkgname}.install


build() {
   cd "${srcdir}"
   msg "Connecting to GIT server...."

   if [ -d ${_gitname} ] ; then
      cd ${_gitname} && git pull origin
      msg "The local files are updated."
   else
      git clone ${_gitroot} ${_gitname}
   fi

   msg "GIT checkout done or server timeout"
   msg "Starting make..."

   rm -rf "${srcdir}/${_gitname}-build"
   git clone "${srcdir}/${_gitname}" "${srcdir}/${_gitname}-build"
   cd "${srcdir}/${_gitname}-build"

   ./configure --prefix=/usr --with-native-plugins --with-python3-plugins
   make
}

package(){
   cd "${srcdir}/${_gitname}-build"
   make DESTDIR="${pkgdir}/" install
   install -Dm644 "${pkgdir}/usr/share/RhythmCat2/images/RhythmCat2_128x128.PNG" "${pkgdir}/usr/share/icons/hicolor/128x128/apps/RhythmCat2.png"
   install -Dm644 "${pkgdir}/usr/share/RhythmCat2/images/RhythmCat2_256x256.PNG" "${pkgdir}/usr/share/icons/hicolor/256x256/apps/RhythmCat2.png"
   install -Dm644 "${srcdir}/RhythmCat2.desktop" "${pkgdir}/usr/share/applications"
}
