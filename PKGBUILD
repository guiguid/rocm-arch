# Maintainer: Jakub Okoński <jakub@okonski.org>
pkgname=roct-thunk-interface
pkgver=2.1.0
pkgrel=1
pkgdesc="ROCm HSA"
arch=(x86_64)
url="https://github.com/RadeonOpenCompute/ROCT-Thunk-Interface"
license=('unknown')
makedepends=(git cmake gcc ninja) 
depends=(numactl)
source=("git+https://github.com/RadeonOpenCompute/ROCT-Thunk-Interface.git#tag=roc-2.1.0" "fix_build-dev_command.patch")
sha256sums=("SKIP" "bbbc02908fdde51b46eb87f1ee68d0d6172aa83f76f7eaed4bf4e2eb17633615")

prepare() {
    cd ROCT-Thunk-Interface
    patch -Np1 -i "${srcdir}/fix_build-dev_command.patch"
}

build() {
  mkdir -p $srcdir/build
  cd $srcdir/build
  cmake -DCMAKE_BUILD_TYPE=Release \
        -DCMAKE_INSTALL_PREFIX=$pkgdir/opt/rocm \
        -G Ninja \
        $srcdir/ROCT-Thunk-Interface
  ninja all build-dev
}

package() {
  ninja -C $srcdir/build install install-dev
  mkdir -p $pkgdir/etc/ld.so.conf.d
  cat <<-EOF > $pkgdir/etc/ld.so.conf.d/roct-thunk-interface.conf
		/opt/rocm/lib64
		EOF
}

