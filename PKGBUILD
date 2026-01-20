pkgname=as21xxx-dkms
pkgver=2026.01.07.1.r2.gf1b8ec8
pkgrel=1
pkgdesc="Aeonsemi AS21xxx PHY Driver DKMS"
arch=(any)
url="https://github.com/MollySophia/as21xxx-dkms"
license=('GPL-2.0-or-later')
depends=(dkms)
makedepends=(rsync)
options=(!strip !debug)
source=(PKGBUILD)
sha256sums=(SKIP)

pkgver() {
	realdir=$(dirname $(realpath $srcdir/PKGBUILD))
	cd ${realdir}
	ver="$(git describe --tags 2>/dev/null | sed 's/^[vV]//;s/\([^-]*-g\)/r\1/;s/-/./g')"
	if [ -z "$ver" ]; then
		cnt="$(git rev-list --count HEAD)"
		rev="$(git rev-parse --short HEAD)"
		printf "r%s.%s" "$cnt" "$rev"
	else
		printf "%s" "$ver"
	fi
}

package() {
	realdir=$(dirname $(realpath $srcdir/PKGBUILD))
	rsync --verbose --recursive --mkpath --exclude-from="$realdir/.gitignore" \
		"$realdir/dkms.conf" \
		"$realdir/drivers" \
		"$pkgdir/usr/src/$pkgname-$pkgver/"
	sed -i \
		-e "s,^PACKAGE_VERSION=\".*\"$,PACKAGE_VERSION=\"$pkgver\",g" \
		-e "s,^PACKAGE_NAME=\".*\"$,PACKAGE_NAME=\"$pkgname\",g" \
		"$pkgdir/usr/src/$pkgname-$pkgver/dkms.conf"
}
