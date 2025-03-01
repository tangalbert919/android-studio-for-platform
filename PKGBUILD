pkgname=android-studio-for-platform
pkgver=2024.2.2.13
pkgrel=2
pkgdesc="The official Android IDE for Platform"
arch=('i686' 'x86_64')
url="https://developer.android.com/"
license=('APACHE')
makedepends=()
depends=('alsa-lib' 'freetype2' 'libxrender' 'libxtst' 'which')
optdepends=('gtk2: GTK+ look and feel'
            'libgl: emulator support'
            'ncurses5-compat-libs: native debugger support')
options=('!strip')
source=("https://dl.google.com/dl/android/asfp/asfp-Ladybug%20Feature%20Drop-$pkgver-linux.deb"
        "$pkgname.desktop"
        "license.html")
sha256sums=('c8c51358ea581dafc08b3ae0becfe66e87eb0eaadb2f96c9623ba494877253fd'
            '50e03b64971a2d0cc631e0276470bf66464f60b3b86b0a89fb8f532c752a42de'
            'f7b9a49e5f563321b5fce2c8c8bb71a4f07ce886c8772ed5dd4aeb63546a7a5b')

if [ "$CARCH" = "i686" ]; then
    depends+=('java-environment')
fi

package() {
  bsdtar -xf data.tar.gz -C "$pkgdir/"
  mv $pkgdir/tmp $pkgdir/opt
  mv "${pkgdir}/opt/${pkgname}-Stable.2.13" "${pkgdir}/opt/${pkgname}"

  # Install the application
  install -d $pkgdir/{opt/$pkgname,usr/bin}
  #cd $pkgdir
  #cp -a opt/bin opt/lib opt/jbr opt/plugins opt/license opt/LICENSE.txt opt/build.txt opt/product-info.json $pkgdir/opt/$pkgname
  ln -s /opt/$pkgname/bin/studio $pkgdir/usr/bin/$pkgname

  # Copy licenses
  install -Dm644 $pkgdir/opt/$pkgname/LICENSE.txt "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE.txt"
  install -Dm644 $srcdir/license.html "${pkgdir}/usr/share/licenses/${pkgname}/license.html"

  # Add the icon and desktop file
  install -Dm644 $pkgdir/opt/$pkgname/bin/studio.png $pkgdir/usr/share/pixmaps/$pkgname.png
  install -Dm644 $srcdir/$pkgname.desktop $pkgdir/usr/share/applications/$pkgname.desktop

  chmod -R ugo+rX $pkgdir/opt
}