# Maintainer: Niklp

_pkgname=nik
pkgname=nik-theme
pkgver=r.
pkgrel=1
pkgdesc="Nik's KDE Plasma theme"
# provides=('plasma5-themes-breath' 'sddm-breath-theme')
arch=('any')
url="https://github.com/Niklp09/nik-theme"
license=('LGPL')
depends=('breeze' 'plasma-framework' 'plasma-workspace')
makedepends=('extra-cmake-modules' 'git' 'plasma-framework')
source=("git+$url.git")
sha256sums=('SKIP')

pkgver() {
  cd "$srcdir/$_pkgname"
  echo r$(git rev-list --count master).$(git rev-parse --short master)
}

prepare() {
  mkdir -p build
}

build() {
  cd build
  cmake ../$_pkgname \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DKDE_INSTALL_USE_QT_SYS_PATHS=ON \
  make
}

package() {
  cd build
  make DESTDIR="${pkgdir}" install
}
