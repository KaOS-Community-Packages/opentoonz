pkgname=opentoonz
pkgver=1.1.2.70
pkgrel=1
_commit=a83fb7a965d3b36c7feba8a9781d8066fe84c3c8
pkgdesc="2D Animation software"
arch=('x86_64')
url="https://github.com/opentoonz/opentoonz"
license=('custom')
depends=(
    'gcc' 'gcc-libs' 'boost' 'boost-libs'
    'qt5-base' 'qt5-svg' 'qt5-script' 'qt5-tools' 'qt5-multimedia'
    'sdl2' 'libpng' 'lzo2' 'freetype2' 'gsl' 'lapack'
    'lz4' 'libusb' 'libjpeg-turbo' 'glew' 'freeglut'
    'superlu'
)
makedepends=('cmake')
source=(
    "opentoonz.zip::https://github.com/opentoonz/opentoonz/archive/{$_commit}.zip"
    'LICENSE'
    'opentoonz.desktop'
    'opentoonz.png'
    'opentoonz'
)
md5sums=(
    'b9a0ef2d68b7f274d8aac9adcbd7ac2d'
    '1d0fa18b46a9fbc928e04aaa7d707047'
    '9b83ce34c82746de377a35068628f43f'
    '341056ede09b44b290e2aa46f25f127f'
    '11176431cc99b57c875b0f8c6c57c1c4'
)

prepare() {
    cd "${srcdir}/opentoonz-${_commit}/thirdparty/tiff-4.0.3"
    ./configure --with-pic --disable-jbig
    make
    
    cd "${srcdir}/opentoonz-${_commit}/toonz"
    mkdir -p build
}

build() {
    cd "${srcdir}/opentoonz-${_commit}/toonz/build"
    cmake ../sources -DCMAKE_INSTALL_PREFIX=/usr
    make
}

package() {
    cd "${srcdir}/opentoonz-${_commit}/toonz/build"
    make DESTDIR="${pkgdir}/" install
    install -dm755 "${pkgdir}/usr/share/licenses/opentoonz"
    install -m644 "${srcdir}/LICENSE" "${pkgdir}/usr/share/licenses/opentoonz"
    install -dm755 "${pkgdir}/usr/share/applications"
    install -m644 "${srcdir}/opentoonz.desktop" "${pkgdir}/usr/share/applications"
    install -dm755 "${pkgdir}/usr/share/icons/hicolor/32x32/apps"
    install -m644 "${srcdir}/opentoonz.png" "${pkgdir}/usr/share/icons/hicolor/32x32/apps"
    install -dm755 "${pkgdir}/usr/bin"
    install -m755 "${srcdir}/opentoonz" "${pkgdir}/usr/bin"
}
