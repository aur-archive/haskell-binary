# $Id: PKGBUILD 72251 2012-06-11 04:32:01Z tdziedzic $
# Maintainer: Alexander Rødseth <rodseth@gmail.com>
# Contributor: Vesa Kaihlavirta <vesa@archlinux.org>
# Contributor: Arch Haskell Team <arch-haskell@haskell.org>

pkgname=haskell-binary
pkgver=0.5.1.0
pkgrel=2
pkgdesc="Binary serialisation for Haskell values using lazy ByteStrings"
url="http://hackage.haskell.org/package/binary"
license=('custom:BSD3')
arch=('x86_64' 'i686')
depends=('ghc=7.4.2-1' sh)
options=('strip')
source=("http://hackage.haskell.org/packages/archive/binary/$pkgver/binary-$pkgver.tar.gz")
install=haskell-binary.install
sha256sums=('2ad477b47e9158d61517689f5f0c7b0240ff891059418d6758879020800351a3')

build() {
  cd "$srcdir/binary-$pkgver"

  runhaskell Setup configure -O -p --enable-split-objs --enable-shared \
    --prefix=/usr --docdir="/usr/share/doc/$pkgname" \
    --libsubdir=\$compiler/site-local/\$pkgid
  runhaskell Setup build
  runhaskell Setup haddock
  runhaskell Setup register --gen-script
  runhaskell Setup unregister --gen-script
  sed -i -r -e "s|ghc-pkg.*unregister[^ ]* |&'--force' |" unregister.sh
}

package() {
  cd "$srcdir/binary-$pkgver"

  install -Dm 744 register.sh \
    "$pkgdir/usr/share/haskell/$pkgname/register.sh"
  install -m 744 unregister.sh \
    "$pkgdir/usr/share/haskell/$pkgname/unregister.sh"
  install -dm 755 "$pkgdir/usr/share/doc/ghc/html/libraries"
  ln -s "/usr/share/doc/$pkgname/html" \
    "$pkgdir/usr/share/doc/ghc/html/libraries/binary"
  runhaskell Setup copy --destdir="$pkgdir"
  install -Dm 644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  rm -f "$pkgdir/usr/share/doc/$pkgname/LICENSE"
}

# vim:set ts=2 sw=2 et:
