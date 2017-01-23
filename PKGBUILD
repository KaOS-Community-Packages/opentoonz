pkgname=opentoonz
pkgver=1.1.2.4a76fd8
pkgrel=1
pkgdesc="2D Animation software."
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
makedepends=('cmake' 'git')
install=opentoonz.install
source=(
    'git+https://github.com/opentoonz/opentoonz.git#commit=4a76fd864fcbf5a7cb75011538df2cbc05fee5a1'
    'LICENSE'
    'opentoonz.install'
    'opentoonz.desktop'
    'opentoonz.png'
)
md5sums=(
    'SKIP'
    '1d0fa18b46a9fbc928e04aaa7d707047'
    '970ce10aac6dcd32cedb4c5f96977cea'
    'b6e5170ba3f89d9ef349c0e527a319d9'
    '341056ede09b44b290e2aa46f25f127f'
)

prepare() {
    cd "${srcdir}/opentoonz/thirdparty/tiff-4.0.3"
    ./configure --with-pic --disable-jbig
    make
    
    cd "${srcdir}/opentoonz/toonz"
    mkdir -p build
}

build() {
    cd "${srcdir}/opentoonz/toonz/build"
    cmake ../sources -DCMAKE_INSTALL_PREFIX=/usr
    make
}

package() {
    cd "${srcdir}/opentoonz/toonz/build"
    make DESTDIR="${pkgdir}/" install
    install -dm755 "${pkgdir}"/usr/share/licenses/opentoonz
    install -m644 ../../../LICENSE "${pkgdir}"/usr/share/licenses/opentoonz
    install -dm755 "${pkgdir}"/usr/share/applications
    install -m644 ../../../opentoonz.desktop "${pkgdir}"/usr/share/applications
    install -dm755 "${pkgdir}"/usr/share/icons/hicolor/32x32/apps
    install -m644 ../../../opentoonz.png "${pkgdir}"/usr/share/icons/hicolor/32x32/apps
}
