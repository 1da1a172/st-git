# Maintainer: mar77i <mar77i at mar77i dot ch>
# Past Maintainer: Gaetan Bisson <bisson@archlinux.org>
# Contributor: Scytrin dai Kinthra <scytrin@gmail.com>

pkgname=st-git
_pkgname=st
pkgver=0.8.2.1.ge85b6b6
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
sha1sums=('SKIP'
          '3969ca419d9fecb2b356905d8522867a0fd8565a'
          '4cfc4bad41e4988aa3da838ecbf9926eac745364'
          'ac5eb20239a2b257aaaa045849aa5d7f62632a70'
          'dcad090a5f4f9510da6157524cd1eb97979e3af5'
          'a6e4efb0386e4deaec3f4d77f167a2d6e90ab45e'
          'c5b6b70e41bdd3953a1df3c06a3c541b53419291'
          '55a218d7bd8002c143c8cd176da394a58091841d')

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
