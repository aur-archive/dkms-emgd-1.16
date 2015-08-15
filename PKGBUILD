# Maintainer: Gustavo Alvarez <sl1pkn07@gmail.com>

pkgname=dkms-emgd-1.16
_pkgname=dkms-emgd
pkgver=1.16.3196
pkgrel=4
pkgdesc="Intel EMGD driver in DKMS format."
arch=('i686')
url="http://edc.intel.com/Software/Downloads/EMGD/"
license=('GPL')
depends=('dkms' 'xorg-server')
makedepends=('make' 'bash' 'patch')
provides=('emgd')
install="dkms-emgd.install"

source=(http://www.fit-pc2.com/download/mint/fitpc2/maya/emgd-dkms_${pkgver}.deb
        ${_pkgname}.install
        emgd-3.6-fix.patch
        emgd-3.7-fix.patch
        emgd-3.8-fix.patch)
md5sums=('3686bdb82caaddd120242f7a53264430'
         '39aa7d5ab9afb27db27887c0a8dd623c'
         '62549a424e4afcf6e19a58c530b07f79'
         'c5c895f662e91a53ac44308b9e10e10a'
         '40502fa01babaa548075f478f9e1e221')

build() {
    # Messages
    warning "This Driver NEED using Xorg 1.9."
    echo
    echo '
    Please, edit your /etc/pacman.conf and add:

    [xorg19]
    Server = http://catalyst.apocalypsus.net/repo/xorg19/$arch

    Downgrade all your xorg with packages in Xorg19 repo
    (if need older dependencies, try "http://arm.konnichi.com/extra/os/i686/" 
     
        
    and add to "IgnoreGroup" secction:

    IgnoreGroup = xorg

    to prevent possible upgrade
'
    read -p "If you apply this, please continue, if not, cancel this installation [y/N] " -n 1
      if [[ ! $REPLY =~ ^[Yy]$ ]]; then
	echo
	return 1
      fi
      echo

    cd "${srcdir}"
    tar xzf data.tar.gz
    patch -p0 -i "${srcdir}/emgd-3.6-fix.patch"
    patch -p0 -i "${srcdir}/emgd-3.7-fix.patch"
    patch -p0 -i "${srcdir}/emgd-3.8-fix.patch"
}

package() {
    install -d "${pkgdir}"/usr/src/emgd-"${pkgver}"/
    cp -R "${srcdir}"/usr/src/emgd-${pkgver}/* "${pkgdir}"/usr/src/emgd-"${pkgver}"/
    install -Dm644 "${srcdir}"/usr/src/emgd-${pkgver}/dkms.conf "${pkgdir}"/usr/src/emgd-"${pkgver}"/
    install -Dm755 "${srcdir}"/usr/src/emgd-${pkgver}/COPYING "${pkgdir}"/usr/share/licenses/"${_pkgname}"/COPYING
    rm -fr "${pkgdir}"/usr/src/"${_modname}"-"${pkgver}"/debian
}
