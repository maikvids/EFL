pkgname=('efl')
pkgver=1.17.1
pkgrel=1
pkgdesc="Enlightenment Foundation Libraries"
arch=('x86_64')
url="http://www.enlightenment.org"
license=('BSD' 'LGPL2.1' 'GPL2' 'custom')
depends=('avahi' 'bullet' 'curl' 'harfbuzz' 'fribidi' 'gstreamer' 
         'gst-plugins-base' 'gst-plugins-good' 'gst-plugins-bad' 
         'luajit' 'libjpeg-turbo' 'libpng' 'libpulse' 'libtiff' 
         'libxcomposite' 'libxinerama' 'libxrandr' 'libxss' 'libinput'
         'libxcursor' 'libxp' 'libwebp' 'lz4' 'libxkbcommon' 
         'openjpeg' 'shared-mime-info' 'wayland' 'zlib')
makedepends=('doxygen' 'python2' 'texlive-core' 'ghostscript')
source=("http://download.enlightenment.org/rel/libs/${pkgname}/$pkgname-$pkgver.tar.gz")
md5sums=('e9bd036344cdac8f0e4f996391604d4d')

build() {
  cd "${srcdir}/${pkgname}-${pkgver}"

  export CFLAGS="$CFLAGS -fvisibility=hidden"

  ./configure --prefix=/usr \
  --disable-static --disable-tslib --enable-fb \
  --enable-xinput22 --enable-multisense --enable-systemd \
  --enable-image-loader-webp --enable-harfbuzz --enable-wayland \
  --enable-liblz4 --enable-drm

  make
}

package_efl(){
  cd "${srcdir}/${pkgname}-${pkgver}"
  make -j1 DESTDIR=${pkgdir} install

  # install non-standard license files
  install -Dm644 "${srcdir}/${pkgname}-${pkgver}/licenses/COPYING.BSD" \
    "${pkgdir}/usr/share/licenses/${pkgname}/COPYING.BSD"
  install -Dm644 "${srcdir}/${pkgname}-${pkgver}/licenses/COPYING.SMALL" \
    "${pkgdir}/usr/share/licenses/${pkgname}/COPYING.SMALL"
}
