# Maintainer: mar77i <mar77i at mar77i dot ch>
# Past Maintainer: Gaetan Bisson <bisson@archlinux.org>
# Contributor: Scytrin dai Kinthra <scytrin@gmail.com>

pkgname=st-git
_pkgname=st
pkgver=0.8.2.25.g3848301
pkgrel=2
pkgdesc='Simple virtual terminal emulator for X'
url='http://st.suckless.org/'
arch=('i686' 'x86_64')
license=('MIT')
options=('zipman')
depends=('libxft')
makedepends=('ncurses' 'libxext' 'git')
epoch=1
# include config.h and any patches you want to have applied here
source=('git://git.suckless.org/st'
	'0001-use-anonymous-pro.patch'
	'0002-smaller-boarder.patch'
	'0003-actionfps-to-120.patch'
	'0004-use-modified-ir_black-color-scheme.patch'
	'0005-zoom-by-2.patch'
	'0006-change-zoom-shortcuts.patch'
	'0007-set-tabspaces-to-4.patch')
sha256sums=('SKIP'
            '2aee25ac14419f927753ad59805c68e30d4e78fe4681b1209b0e284266031aa4'
            '053fa87aa98eb8ecda5013bcb5d035534a7a3265de74fe62df114f0e9fc829f2'
            '7a92fe2dac6cce1edfa8f5747cba2f7d21bf764da0edcc528f509397d57a48a5'
            '5d6acc5ebc604e29ecdacbe2ce2ef2629d709a63b5e4f41a294f2a0e52f2acbc'
            'e7ca004fc284907b21ee29f2ac69e8361a4bc29327de366a6503d99e34b27daf'
            '2a19627cfa2c6e7d83653b6b67a4867aac5090662ae4c10573acf20bd97a2e7e'
            'c8be5f8e8b01cb48babf3ebd77a7f22c63d7ad9fb61c273ab403cac51ca83ac6')

provides=("${_pkgname}")
conflicts=("${_pkgname}")

pkgver() {
	cd "${_pkgname}"
	git describe --tags |sed 's/-/./g'
}

prepare() {
	local file
	cd "${_pkgname}"
	for file in "${source[@]}"; do
		if [[ "$file" == "config.h" ]]; then
			cp "$srcdir/$file" .
		elif [[ "$file" == *.diff || "$file" == *.patch ]]; then
			# add all patches present in source array
			patch -Np1 <"$srcdir/$(basename ${file})"
		fi
	done
}

build() {
	cd "${_pkgname}"
	make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11
}

package() {
	cd "${_pkgname}"
	make PREFIX=/usr DESTDIR="${pkgdir}" install
	install -Dm644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
	install -Dm644 README "${pkgdir}/usr/share/doc/${pkgname}/README"
}
