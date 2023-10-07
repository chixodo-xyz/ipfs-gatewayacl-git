# Maintainer: Josias <aur at macherstube dot ch>
_pkgname=ipfs-gatewayacl
pkgname=$_pkgname-git
pkgver=0.0.2.r0.g9e0c226
pkgrel=1
pkgdesc="Gateway ACL for IPFS (Kubo)"
arch=('x86_64')
url="https://github.com/chixodo-xyz/ipfs-gatewayacl"
license=('GPL3')
groups=()
depends=('openresty')
makedepends=(git)
optdepends=()
provides=("$_pkgname")
conflicts=("$_pkgname")
replaces=()
backup=()
options=()
install='prod.install'
source=('git+https://github.com/chixodo-xyz/ipfs-gatewayacl.git')
noextract=()
b2sums=('SKIP')

prepare() {
	cd "$srcdir/$_pkgname"
	version=$(git describe --tags --abbrev=0)
	printf "\033[34;1mPrepare ipfs-gatewayacl %s (%s)\n\033[0m" ${version} $(git describe --long --tags --abbrev=7 --match="v*" HEAD |
		sed 's/^v//;s/\([^-]*-g\)/r\1/;s/-/./g')
	git config advice.detachedHead false
	git checkout ${version} -f
	if [ $? -ne 0 ]; then
		printf "\033[31;1mTag not found.\n\033[0m"
		exit -1
	fi
}

pkgver() {
	cd "$srcdir/$_pkgname"
	git describe --long --tags --abbrev=7 --match="v*" HEAD |
		sed 's/^v//;s/\([^-]*-g\)/r\1/;s/-/./g'
}

build() {
	printf "\033[0;33mNo building required...\n\033[0m"
}

check(){
	printf "\033[0;33mNo checking required...\n\033[0m"
}

package() {
	printf "\033[34;1mCreate Package\n\033[0m"

	cd "$srcdir/$_pkgname"
	sourceDir=`realpath "$srcdir/$_pkgname"`
	luaDir="/lib/lua/5.1"
	configDir="/etc/$_pkgname"
	destDir="/usr/share/$_pkgname"
	binaryDir="/usr/bin/"

	printf "Source: %s\n" $sourceDir
	printf "Destination: %s\n" $pkgdir

	printf "\033[34;1mPrepare folders\n\033[0m"
	printf "LuaLib: %s\n" "$pkgdir$luaDir"
	mkdir -p "$pkgdir$luaDir"
	printf "Config: %s\n" "$pkgdir$configDir"
	mkdir -p "$pkgdir$configDir"
	printf "Dest:   %s\n" "$pkgdir$destDir"
	mkdir -p "$pkgdir$destDir"
	printf "Binary: %s\n" "$pkgdir$binaryDir"
	mkdir -p "$pkgdir$binaryDir"

	printf "\033[34;1mPopulating folders\n\033[0m"
	cp $sourceDir/lib/* $pkgdir$luaDir/
	cp $sourceDir/config/* $pkgdir$configDir/
	cp $sourceDir/src/* $pkgdir$destDir/
}
