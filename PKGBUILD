pkgname=st
pkgver=0.8.1
pkgrel=1
pkgdesc='A simple virtual terminal emulator for X.'
arch=('i686' 'x86_64')
license=('MIT')
depends=('libxft' 'libxext')
makedepends=('ncurses')
url="http://st.suckless.org"

_patches=("https://st.suckless.org/patches/clipboard/st-clipboard-0.8.1.diff")

source=("http://dl.suckless.org/st/$pkgname-$pkgver.tar.gz"
        "config.h"
        "${_patches[@]}")

sha256sums=('c4fb0fe2b8d2d3bd5e72763e80a8ae05b7d44dbac8f8e3bb18ef0161c7266926'
            '3dc36bbb2f022428fec77b7adf752e965b75eab32e067f1cf73b553ba653b476'
            'f22e0165aacb2bc86d000728c81f68022abcc601dbfd09e516e1ba772225d7e6')

prepare() {
  cd $srcdir/$pkgname-$pkgver
  # skip terminfo which conflicts with nsurses
  sed -i '/\ttic -sx st.info/d' Makefile

  for patch in "${_patches[@]}"; do
    echo "Applying patch $(basename $patch)..."
    patch -Np1 -i "$srcdir/$(basename $patch)"
  done

  cp $srcdir/config.h config.h
}

build() {
  cd $srcdir/$pkgname-$pkgver
  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11
}

package() {
  cd $srcdir/$pkgname-$pkgver
  make PREFIX=/usr DESTDIR="$pkgdir" TERMINFO="$pkgdir/usr/share/terminfo" install
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  install -Dm644 README "$pkgdir/usr/share/doc/$pkgname/README"
}
