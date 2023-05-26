# Maintainer: Jonathan Steel <jsteel at archlinux.org>
# Contributor: Benjamin Klettbach <b.klettbach@gmail.com>

pkgname=obs-studio
pkgver=29.1.1
pkgrel=2
pkgdesc="Free, open source software for live streaming and recording"
arch=('x86_64')
url="https://obsproject.com"
license=('GPL2')
depends=('ffmpeg' 'jansson' 'libxinerama' 'libxkbcommon-x11' 'mbedtls' 'rnnoise' 'pciutils'
         'qt6-svg' 'curl' 'jack' 'gtk-update-icon-cache' 'pipewire' 'libxcomposite' 'websocketpp' 'asio')
makedepends=('cmake' 'libfdk-aac' 'x264' 'swig' 'python' 'luajit' 'sndio')
optdepends=('libfdk-aac: FDK AAC codec support'
            'libva-intel-driver: hardware encoding'
            'libva-mesa-driver: hardware encoding'
            'luajit: scripting support'
            'python: scripting support'
            'sndio: Sndio input client'
            'v4l2loopback-dkms: virtual camera support')
source=($pkgname-$pkgver.tar.gz::https://github.com/tbocek/obs-source-all/releases/download/$pkgver/obs-studio-$pkgver.tar.gz
        fix_python_binary_loading.patch
        ignore_unused_submodules.patch)
sha256sums=('e329ffca56d0dada9758e28484195ebb3628d76210f574bc326dd3bd22a540e0'
            'bdfbd062f080bc925588aec1989bb1df34bf779cc2fc08ac27236679cf612abd'
            '60b0ee1f78df632e1a8c13cb0a7a5772b2a4b092c4a2a78f23464a7d239557c3')

prepare() {
  cd $pkgname-$pkgver
  patch -Np1 < "$srcdir"/fix_python_binary_loading.patch
  patch -Np1 < "$srcdir"/ignore_unused_submodules.patch
}

build() {
  cmake -B build -S $pkgname-$pkgver \
    -DCMAKE_INSTALL_PREFIX="/usr" \
    -DENABLE_BROWSER=OFF \
    -DENABLE_VST=ON \
    -DENABLE_VLC=OFF \
    -DENABLE_NEW_MPEGTS_OUTPUT=OFF \
    -DENABLE_AJA=OFF \
    -DENABLE_JACK=ON \
    -DENABLE_LIBFDK=ON \
    -DOBS_VERSION_OVERRIDE="$pkgver-$pkgrel" \
    -Wno-dev
  cmake --build build
}

package() {
  DESTDIR="$pkgdir" cmake --install build
}
