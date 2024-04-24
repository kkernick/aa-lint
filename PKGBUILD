pkgname=aa-lint-git
pkgdesc="Lint AppArmor Profiles"
pkgver=r2.eb40d9a
pkgrel=1

source=("git+https://github.com/kkernick/aa-lint.git")
sha256sums=("SKIP")
depends=(python python-termcolor)
arch=("any")
provides=("aa-lint")

pkgver() {
	cd $srcdir/aa-lint
	printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short=7 HEAD)"
}

package() {
	cd $srcdir/aa-lint
	for binary in aa-lint; do
		install -Dm755 "$binary" "$pkgdir/usr/bin/$binary"
	done
}
