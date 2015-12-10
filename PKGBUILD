pkgname=unified-remote-server
_pkgname=urserver
pkgver=3.3.4.734
pkgrel=2
pkgdesc='Unified Remote Server for Linux. Easily the best way of controlling your PC from your smartphone.'
arch=('x86_64')
url="https://www.unifiedremote.com"
license=('Unified Intents AB')
install=$pkgname.install
depends=("libx11" "libxext" "libstdc++5")
optdepends=('bluez' 'bluez-libs: To Enable the Bluetooth Protocol')
source=("https://www.unifiedremote.com/static/builds/server/linux-x64/734/${_pkgname}-${pkgver}.deb" "urserver.service")
md5sums=('f8bf2ece6c2d2cf8c3968afe620bfb67' '4137536d9b6171e30d311ab32da2d029')

package() {
  cd "${srcdir}"

	tar -xzf data.tar.gz

	#fix desktop file
	sed -i -e '9,24d;26d' $(find . -name 'urserver.desktop')

        # opt,usr Sources
	install -d "${pkgdir}"/opt/urserver
        cp -r {opt,usr} "${pkgdir}/"
        
        # clean up permissions
	find "${pkgdir}" -type d | xargs -I {} chmod -R 755 "{}"
	find "${pkgdir}" -type f | xargs -I {} chmod -R 644 "{}"
	chmod 755 "${pkgdir}/opt/urserver/urserver"
	chmod 755 "${pkgdir}/opt/urserver/urserver-start"
	chmod 755 "${pkgdir}/opt/urserver/urserver-stop"
    
	# add service systemd
        install -Dm644 "urserver.service" "$pkgdir/usr/lib/systemd/system/urserver.service"
}
