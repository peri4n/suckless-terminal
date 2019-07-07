pkgname=st
pkgver=0.8.2
pkgrel=1
pkgdesc='A simple virtual terminal emulator for X.'
arch=('i686' 'x86_64')
license=('MIT')
depends=('libxft' 'libxext' 'xurls')
makedepends=('ncurses')
url="http://st.suckless.org"

source=("http://dl.suckless.org/st/$pkgname-$pkgver.tar.gz"
        "config.h"
        "1-st-0.8.2-externalpipe.diff"
        "2-st-0.8.2-clipboard.diff")

sha256sums=('aeb74e10aa11ed364e1bcc635a81a523119093e63befd2f231f8b0705b15bf35'
            'f2b68d26ce4b46bdb59b3f649f8af932da6ac9d506cae8215503c96ad57dfe10'
            'a43e54f36515f846ec662752425859c2784544d3b0be7db1fad4f1791a54480d'
            '7be1a09831f13361f5659aaad55110bde99b25c8ba826c11d1d7fcec21f32945')

prepare() {
  cd $srcdir/$pkgname-$pkgver

  patch -p1 -i ../1-st-0.8.2-externalpipe.diff
  patch -p1 -i ../2-st-0.8.2-clipboard.diff

  cp $srcdir/config.h config.h
}

build() {
  cd $srcdir/$pkgname-$pkgver
  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11
}

package() {
  cd $srcdir/$pkgname-$pkgver
  sed -i '/\@tic /d' Makefile
  make PREFIX=/usr DESTDIR="$pkgdir" TERMINFO="$pkgdir/usr/share/terminfo" install
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  install -Dm644 README "$pkgdir/usr/share/doc/$pkgname/README"
}
