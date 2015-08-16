# Contributor: Francisco Demartino <demartino.francisco@gmail.com>

_realname=opusfile
pkgname="mingw-w64-${_realname}"
pkgver=0.6
pkgrel=4
pkgdesc="Library for opening, seeking, and decoding .opus files (mingw-w64)"
arch=('any')
url="https://www.opus-codec.org/"
license=("BSD")
depends=("mingw-w64-crt"
         "mingw-w64-libogg"
         "mingw-w64-openssl"
         "mingw-w64-opus")
makedepends=("mingw-w64-configure")
options=('!strip' '!buildflags' 'staticlibs')
source=("https://ftp.mozilla.org/pub/mozilla.org/opus/${_realname}-${pkgver}.tar.gz")
md5sums=('3d6705e66375f6205dffdd63b2ad3538')
_architectures="i686-w64-mingw32 x86_64-w64-mingw32"

build() {
  cd "${srcdir}/${_realname}-${pkgver}"
  for _arch in ${_architectures}; do
    mkdir -p "build-${_arch}" && pushd "build-${_arch}"
    ${_arch}-configure --disable-doc
    make
    popd
  done
}

package() {
  for _arch in ${_architectures}; do
    cd "${srcdir}/${_realname}-${pkgver}/build-${_arch}"
    make DESTDIR="${pkgdir}" install

    ${_arch}-strip --strip-unneeded "$pkgdir"/usr/${_arch}/bin/*.dll
    ${_arch}-strip -g "$pkgdir"/usr/${_arch}/lib/*.a

    # Install license
    install -Dm644 ${srcdir}/${_realname}-${pkgver}/COPYING ${pkgdir}/usr/share/licenses/${pkgname}/LICENSE
  done
}
