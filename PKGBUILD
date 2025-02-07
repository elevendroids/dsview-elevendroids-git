epoch=1
pkgname=dsview-elevendroids-git
pkgver=1.3.2.r56.ge3beb76a
pkgrel=1
pkgdesc="Client software that supports the DreamSourceLab logic analyzer"
arch=('i686' 'x86_64')
url="http://www.dreamsourcelab.com/"
license=('GPL3')
depends=('hicolor-icon-theme' 'qt6-base' 'qt6-svg' 'fftw' 'python' 'libusb')
makedepends=('cmake' 'ninja' 'boost')
provides=('dsview')
conflicts=('dsview')

source=(git+https://github.com/elevendroids/DSView)
sha384sums=('SKIP')

pkgver() {
  cd DSView
  git describe --tags | sed -r 's/^v//;s/([^-]*-g)/r\1/;s/-/./g'
}

prepare() {
  sed -i 's#MODE="0666"#TAG+="uaccess"#' \
    "DSView/DSView/DreamSourceLab.rules"
}

build() {
    cmake -B build -S "DSView" \
        -GNinja \
        -DCMAKE_BUILD_TYPE='None' \
        -DCMAKE_INSTALL_PREFIX='/usr' \
        -Wno-dev
    cmake --build build
}

check() {
    ctest --test-dir build --output-on-failure
}

package() {
    DESTDIR="$pkgdir" cmake --install build
}

# vim:set ts=2 sw=2 et:
