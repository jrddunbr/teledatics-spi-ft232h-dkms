pkgname=teledatics-spi-ft232h-dkms
pkgver=1.0.0
pkgrel=1
pkgdesc="Teledatics SPI FT232H DKMS driver for the TD-XPAH development board"
arch=('any')
url=""
license=('BSD'  'GPL2')
depends=('dkms')
source=("${srcdir}/${pkgname}::git+https://github.com/teledatics/spi-ft232h-dkms#commit=1acaf7014185953878428d5395daf828347e8c03" "dkms.conf" "60-spi-ft232h-dkms.rules")
sha256sums=('SKIP' 'b3ef9f7d0557317a42cfbe61081393642b3f54af3960ecd38341f52d02ef7bb9' '8f63da0cff7aa655c3cdfa1c4cae6a9fcdd1b1c381cd7ff388d5debf45ed5929')

prepare() {
    # Disables (blacklists) the FTDI SIO driver. This will disable usage of the standalone mode and serial debugger as a side effect
    echo "blacklist ftdi_sio" > "${srcdir}/blacklist-ftdi_sio.conf"
}

package() {
  # Install source code for dkms
  install -Dm644 "${srcdir}/${pkgname}/src/ft232h-intf.h" "${pkgdir}/usr/src/${pkgname}-${pkgver}/ft232h-intf.h"
  install -Dm644 "${srcdir}/${pkgname}/src/Kconfig" "${pkgdir}/usr/src/${pkgname}-${pkgver}/Kconfig"
  install -Dm644 "${srcdir}/${pkgname}/src/Makefile" "${pkgdir}/usr/src/${pkgname}-${pkgver}/Makefile"
  install -Dm644 "${srcdir}/${pkgname}/src/spi-ft232h.c" "${pkgdir}/usr/src/${pkgname}-${pkgver}/spi-ft232h.c"

  # Install dkms config
  install -Dm644 "${srcdir}/dkms.conf" "${pkgdir}/usr/src/${pkgname}-${pkgver}/dkms.conf"

  # Install udev rules, modprobe files, license
  install -Dm644 "${srcdir}/60-spi-ft232h-dkms.rules" "${pkgdir}/usr/lib/udev/rules.d/60-spi-ft232h-dkms.rules"
  install -Dm644 "${srcdir}/blacklist-ftdi_sio.conf" "${pkgdir}/etc/modprobe.d/blacklist-ftdi_sio.conf"
  install -Dm644 "${srcdir}/${pkgname}/misc/spi-ft232h.conf" "${pkgdir}/etc/modprobe.d/spi-ft232h.conf"
  install -Dm644 "${srcdir}/${pkgname}/debian/copyright" "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}