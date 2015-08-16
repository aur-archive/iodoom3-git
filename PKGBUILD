# Contributor: Slash <demodevil5 [at] yahoo [dot] com>
# Contributor: Andrew Simmons <andrew.simmons@gmail.com>
# Contributor: teddy_beer_maniac <teddy_beer_maniac@wp.pl>
# Contributor: Babets
# Contributor: Paolo Bolzoni
# Maintainer: Behem0th <grantipak at gmail dot com>

pkgname=iodoom3-git
_gitname="iod3"
pkgver=20141221
pkgrel=1
pkgdesc="A fork of the Doom 3 source code as released by id software under the GPLv3 on November 22, 2011. You need the retail .pk4 files to play."
arch=(i686 x86_64)
url="http://www.iodoom3.org/"
license=('GPL')
groups=(games)
if [ "$CARCH" = "i686" ]; then
depends=('libgl' 'alsa-lib' 'openal' 'libxxf86vm' 'libstdc++5')
makedepends=('git' 'scons' 'zip')
optdepends=(
'alsa-plugins: pulseaudio-support'
'libpulse: pulseaudio support'
)
fi
if [ "$CARCH" = "x86_64" ]; then
depends=('lib32-libgl' 'lib32-alsa-lib' 'lib32-openal' 'lib32-libxxf86vm' 'lib32-libstdc++5')
makedepends=('git' 'scons' 'gcc-multilib' 'zip')
optdepends=(
'lib32-alsa-plugins: pulseaudio-support'
'lib32-libpulse: pulseaudio support'
)
fi
provides=("iodoom3")
install=iodoom3.install
source=('git://github.com/iodoom/iod3.git'
        'iodoom3.launcher' 'iodoom3.desktop' 'iodoom3.launcher64' 'iodoom3.png' 'iodoom3.install'
        "http://www.1337-server.net/doom3/doom3-linux-1.3.1.1304.x86.run")
md5sums=('SKIP'
         'ccd29ade9415bc659520315df1f2aa77'
         '86228519a9670155ce31e10ce3b65834'
         'f45bb0c36a4f23a1286d7b790318d98a'
         'f99eb141eecc4b9dd188d6819d741546'
         'f1ee139262037622992d45a1490f0a01'
         '6325f0936f59420d33668754032141cb')

pkgver() {
  date +%Y%m%d
}

build() {
  cd $_gitname/neo
  scons NOCURL=1 BUILD=release BUILD_GAMEPAK=1

  cd $srcdir
  chmod +x $srcdir/doom3-linux-1.3.1.1304.x86.run
  ./doom3-linux-1.3.1.1304.x86.run --tar xf
}

package() {
  install -m 755 -d "$pkgdir"/opt/iodoom3/{base,d3xp}
  install -m 755 $_gitname/neo/doom.x86 "$pkgdir"/opt/iodoom3
  install -m 644 $_gitname/base/default.cfg "$pkgdir"/opt/iodoom3/base
  install -m 644 $_gitname/neo/game01-base.pk4 "$pkgdir"/opt/iodoom3/base/game01.pk4
  install -m 644 $_gitname/neo/game01-d3xp.pk4 "$pkgdir"/opt/iodoom3/d3xp/game01.pk4
  install -m 644 $_gitname/{README.txt,COPYING.txt} "$pkgdir"/opt/iodoom3

  install -m 644 base/pak00*.pk4 "$pkgdir"/opt/iodoom3/base
  install -m 644 d3xp/pak00*.pk4 "$pkgdir"/opt/iodoom3/d3xp
  

  if [ "$CARCH" == "i686" ]; then
    install -D -m 755 $srcdir/iodoom3.launcher \
    $pkgdir/usr/bin/iodoom3
  else
    install -D -m 755 $srcdir/iodoom3.launcher64 $pkgdir/usr/bin/iodoom3
  fi

  install -D -m 644 "$srcdir"/iodoom3.png "$pkgdir"/usr/share/pixmaps/iodoom3.png
  install -D -m 644 "$srcdir"/iodoom3.desktop "$pkgdir"/usr/share/applications/iodoom3.desktop
}
