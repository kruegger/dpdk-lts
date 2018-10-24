pkgname=dpdk-lts
pkgver=17.11.4
pkgrel=1
pkgdesc='A set of libraries and drivers for fast packet processing'
arch=(x86_64 i686)
url='http://dpdk.org'
license=(BSD)
options=(!staticlibs)
depends=(numactl)
makedepends=(linux-headers libpcap)
checkdepends=()
source=(
    "http://fast.dpdk.org/rel/dpdk-$pkgver.tar.xz"
)
sha256sums=(
    '4fae77e22ba6c2a03631ca3f81037f51f0ffa095f14850c4f1c92ee946f5eb85'
)

prepare() {
  cd dpdk-stable-$pkgver
  sed -ri 's,(RTE_APP_TEST=).*,\1n,'         config/common_base
  sed -ri 's,(RTE_BUILD_SHARED_LIB=).*,\1y,' config/common_base
  sed 's|\bpython\b|python2|' -i mk/rte.sdktest.mk
  make T=x86_64-native-linuxapp-gcc config
}

build() {
  cd dpdk-stable-$pkgver
  make T=x86_64-native-linuxapp-gcc
}

check() {
  cd dpdk-stable-$pkgver
  # tests fail
  make test T=x86_64-native-linuxapp-gcc
}

package() {
  cd dpdk-stable-$pkgver
  make DESTDIR="$pkgdir" prefix=/usr sbindir=bin install T=x86_64-native-linuxapp-gcc
  cp -a "$pkgdir"/lib/ "$pkgdir"/usr/ && rm -rf "$pkgdir"/lib/
}
