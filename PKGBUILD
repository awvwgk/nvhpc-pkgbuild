# Maintainer:  Rohit Goswami <rohit.goswami@aol.com>
# Maintainer:  Anton Kudelin <kudelin at protonmail dot com>
# Contributor: eolianoe <eolianoe [at] gmail [DoT] com>

pkgname=nvhpc
_REL_YEAR=2021
_CUDA_VER=11.3
pkgver=21.5
pkgrel=2
pkgdesc='NVIDIA HPC SDK'
arch=('x86_64')
url="https://developer.nvidia.com/hpc-sdk"
license=('custom')
depends=('numactl' 'java-runtime' 'env-modules')
makedepends=('bash')
replaces=('pgi-compilers')
conflicts=('pgi-compilers')
_pkgname="${pkgname}_${_REL_YEAR}_${pkgver//.}_Linux_${arch}_cuda_${_CUDA_VER}"
source=("https://developer.download.nvidia.com/hpc-sdk/$pkgver/$_pkgname.tar.gz"
        "nvhpc.sh")
sha256sums=('c624cdd662099fbde5ca904272ad614ef190577b4bbbf8921e49968f1de6502d'
            '18e141f55230257b7c6ad28d745b409b5f68f8c65490f583cdf30d88aa2a254d')
options=(!strip)

package() {
  cd "$srcdir/$_pkgname"
  export NVHPC_SILENT=true
  export NVHPC_INSTALL_DIR="$pkgdir/opt/nvidia"
  bash ./install

  # Remove references to $pkgdir from module files
  cd "$pkgdir/opt/nvidia/modulefiles"
  find . -type f -exec sed -i "s@$pkgdir@@g" {} \;

  # Install license
  cd "$srcdir/$_pkgname/install_components/Linux_$arch/$pkgver/compilers/license"
  install -Dm644 LICENSE.txt "$pkgdir/usr/share/licenses/$pkgname/LICENSE.txt"

  # Install script to set path
  install -Dm755 "$srcdir/$pkgname.sh" "$pkgdir/etc/profile.d/$pkgname.sh"
}
