pkgname=opentoonz
pkgver=1.1.2.70
pkgrel=2
_commit=fb6d38d59cd981b51316162ca5e2537a127b4e79
pkgdesc="2D Animation software"
arch=('x86_64')
url="https://github.com/opentoonz/opentoonz"
license=('custom')
depends=(
    'gcc' 'gcc-libs' 'boost' 'boost-libs'
    'qt5-base' 'qt5-svg' 'qt5-script' 'qt5-tools' 'qt5-multimedia'
    'sdl2' 'libpng' 'lzo2' 'freetype2' 'gsl' 'lapack'
    'lz4' 'libusb' 'libjpeg-turbo' 'glew' 'freeglut'
    'superlu' 'pngcrush' 'findutils'
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
    '5af9c4c6bf08760bcc942bcd3fc6bde1'
    '1d0fa18b46a9fbc928e04aaa7d707047'
    '9b83ce34c82746de377a35068628f43f'
    '341056ede09b44b290e2aa46f25f127f'
    '11176431cc99b57c875b0f8c6c57c1c4'
)

prepare() {
    echo "checking for png errors"
    FILES=$(find "${srcdir}" -type f -iname '*.png')
    FIXED=0
    for f in $FILES; do
        WARN=$(pngcrush -n -warn "$f" 2>&1)
        if [[ "$WARN" == *"PCS illuminant is not D50"* ]] || [[ "$WARN" == *"known incorrect sRGB profile"* ]]; then
            pngcrush -s -ow -rem allb -reduce "$f"
            FIXED=$((FIXED + 1))
        fi
    done
    echo "$FIXED errors detected and fixed"

    cd "${srcdir}/opentoonz-${_commit}/thirdparty/tiff-4.0.3"
    ./configure --with-pic --disable-jbig
    make
    
    cd "${srcdir}/opentoonz-${_commit}/toonz"
    mkdir -p build
}

build() {
    cd "${srcdir}/opentoonz-${_commit}/toonz/build"
    cmake ../sources -DCMAKE_INSTALL_PREFIX=/usr -DWITH_SYSTEM_SUPERLU=1 -DWITH_SYSTEM_LZO=1
    make
}

package() {
    cd "${srcdir}/opentoonz-${_commit}/toonz/build"
    make DESTDIR="${pkgdir}" install
    install -Dm644 "${srcdir}/LICENSE" "${pkgdir}/usr/share/licenses/opentoonz/LICENSE"
    install -Dm644 "${srcdir}/opentoonz.desktop" "${pkgdir}/usr/share/applications/opentoonz.desktop"
    install -Dm644 "${srcdir}/opentoonz.png" "${pkgdir}/usr/share/icons/hicolor/32x32/apps/opentoonz.png"
    install -Dm755 "${srcdir}/opentoonz" "${pkgdir}/usr/bin/opentoonz"
}
