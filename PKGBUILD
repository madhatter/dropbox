# Maintainer: Massimiliano Torromeo <massimiliano.torromeo@gmail.com>
# Contributor: Tom < tomgparchaur at gmail dot com >

pkgname=dropbox
pkgver=2.0.5
pkgrel=1
pkgdesc="A free service that lets you bring your photos, docs, and videos anywhere and share them easily."
arch=("i686" "x86_64")
url="http://www.dropbox.com"
license=(custom)
depends=("dbus-glib" "gtk2" "libsm")
conflicts=("dropbox-experimental")
options=('!strip' '!upx')

_source_arch="x86"
[ "$CARCH" = "x86_64" ] && _source_arch="x86_64"

sha256sums=('84b9d8c82d389dc9b71c13283c2467cdeddeb0fda60d61e1164dacf3bcc4f52f'
            '8b8af2d6a5786d7fa259660a34c47fa0a7534cd112e70d71ee53b1f786baf530'
            'dd8fdb362c0bba8d789010594f021671ff00e535fc75e13da855f43bc7a4b3aa'
            'b9e020c378c318e72857bb6cd859c74e8da1300f34cee5bfec89c4f7a89770a9'
            'c7253ef6806b7efdec6f3d7e1eeaa90f48813e80715733ab9c902123edfdae27'
			'18526d0dc4444e01cc42565e1b46990a3d0b7dcb2f117e5b5064857bcb83bcee')
[ "$CARCH" = "x86_64" ] && sha256sums[0]='326ce4c1dea4d9174be087a5a8f6705ad156da57dd22111bd0507740c675e65c'

source=("https://dl-web.dropbox.com/u/17/${pkgname}-lnx.${_source_arch}-${pkgver}.tar.gz"
        "dropbox.png"
        "dropbox.desktop"
        "terms.txt"
        "dropbox.service")
_patches=(dropboxd.diff)
source=(${source[@]} ${_patches[@]})

package() {
	install -d "$pkgdir/opt"
	cp -R "$srcdir/.dropbox-dist" "$pkgdir/opt/dropbox"

	find "$pkgdir/opt/dropbox/" -type f -exec chmod 644 {} \;
	chmod 755 "$pkgdir/opt/dropbox/dropboxd"
	chmod 755 "$pkgdir/opt/dropbox/dropbox"


	install -d "$pkgdir/usr/bin"

	cd $pkgdir/opt/dropbox
	for p in "${_patches[@]}"; do
      echo "=> $p"
      patch < $srcdir/$p || return 1
    done 
	cd $srcdir

	ln -s "$pkgdir/opt/dropbox/dropboxd" "$pkgdir/usr/bin/dropboxd"

	install -Dm644 "$srcdir/dropbox.desktop" "$pkgdir/usr/share/applications/dropbox.desktop"
	install -Dm644 "$srcdir/dropbox.png" "$pkgdir/usr/share/pixmaps/dropbox.png"
	install -Dm644 "$srcdir/terms.txt" "$pkgdir/usr/share/licenses/$pkgname/terms.txt"
	install -Dm644 "$srcdir/dropbox.service" "$pkgdir/usr/lib/systemd/system/dropbox@.service"
}
