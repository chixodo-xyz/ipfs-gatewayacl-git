# Maintainer: Josias <aur at macherstube dot ch>
_pkgname=ipfs-gatewayacl
pkgname=$_pkgname-git
pkgver=0.0.5.r0.gae11b95
pkgrel=1
pkgdesc="GatewayACL for IPFS (Kubo)"
arch=('x86_64')
url="https://github.com/chixodo-xyz/ipfs-gatewayacl"
license=('GPL3')
groups=()
depends=('openresty' 'bash')
makedepends=(git)
optdepends=('nano' 'sudo')
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
	printf "\033[34;1mPrepare ipfs-gatewayacl %s (%s)\033[0m\n" ${version} $(git describe --long --tags --abbrev=7 --match="v*" HEAD |
		sed 's/^v//;s/\([^-]*-g\)/r\1/;s/-/./g')
	git config advice.detachedHead false
	git checkout ${version} -f
	if [ $? -ne 0 ]; then
		printf "\033[31;1mTag not found.\033[0m\n"
		exit -1
	fi
}

pkgver() {
	cd "$srcdir/$_pkgname"
	git describe --long --tags --abbrev=7 --match="v*" HEAD |
		sed 's/^v//;s/\([^-]*-g\)/r\1/;s/-/./g'
}

build() {
	printf "\033[0;33mNo building required...\033[0m\n"
}

check(){
	printf "\033[0;33mNo checking required...\033[0m\n"
}

package() {
	printf "\033[34;1mCreate Package\033[0m\n"

	cd "$srcdir/$_pkgname"
	sourceDir=`realpath "$srcdir/$_pkgname"`
	binDir="/usr/local/bin"
	luaLibDir="/opt/openresty/site/lualib"
	destDir="/opt/$_pkgname"

	printf "Source: %s\n" $sourceDir
	printf "Destination: %s\n" $pkgdir

	printf "\033[34;1mPrepare folders\033[0m\n"
	printf "LuaLib: %s\n" "$pkgdir$luaLibDir"
	mkdir -p "$pkgdir$luaLibDir"
	printf "Dest:   %s\n" "$pkgdir$destDir"
	mkdir -p "$pkgdir$destDir"
	mkdir -p "$pkgdir$destDir/src"
	mkdir -p "$pkgdir$destDir/config"

	printf "\033[34;1mPopulating folders\033[0m\n"
	cp $sourceDir/lib/* $pkgdir$luaLibDir/
	cp $sourceDir/src/* $pkgdir$destDir/src/
	cp $sourceDir/config/* $pkgdir$destDir/config/
}
