# Maintainer: Kevin MacMartin <prurigro@gmail.com>
# Contributor: Sébastien Luttringer

_pkgname=archversion
pkgname=$_pkgname-envconfig-git
pkgver=20181118.r99.0cc6f62
pkgrel=2
pkgdesc='Archlinux Version Controller (Git version patched for runtime config using environment variables)'
url='https://github.com/seblu/archversion'
arch=('any')
license=('GPL2')
depends=('python' 'pyalpm' 'python-xdg')
makedepends=('git')

source=(
  "$_pkgname::git+https://github.com/seblu/archversion.git"
  'environment_config.patch'
  'unverified_ssl.patch'
)
sha512sums=('SKIP'
            'd161516ebe0438892414c6897237f4e8c0e8f4343f752dad9405a24e00fddf0db058784d9f49334724416ea7f26d70134370729b4efe3d238ef7e3a91fb98ee2'
            '3877a2b1338f0364e6718e2411c6c4a7388d545a1c54a2a4f321b5f533cba3623d3fa164e13cfc4816fb7d9f13f20337d9d13623a27f10461a9e496e044ce0b5')

replaces=("$_pkgname" "$_pkgname-git")
conflicts=("$_pkgname" "$_pkgname-git")
provides=("$_pkgname" "$_pkgname-git")

pkgver() {
  cd $_pkgname
  printf "%s.r%s.%s" "$(git show -s --format=%ci $_commit | sed 's/\ .*//g;s/-//g')" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare() {
  cd $_pkgname
  patch -p1 < ../environment_config.patch
  patch -p1 < ../unverified_ssl.patch
}

build() {
  cd $_pkgname
  ./bootstrap
  ./configure --prefix=/usr
  make
}

package() {
  cd $_pkgname
  make install DESTDIR="$pkgdir"
}
