# Maintainer: Philipp Schmitt (philipp<at>schmitt<dot>co)

pkgname=wallabag
pkgver=2.1.5
pkgrel=1
pkgdesc='Self hostable application for saving web pages'
arch=('any')
url='http://www.wallabag.org/'
license=('MIT')
depends=(
    'php>=5.3.3'
    'php-gd'
    'php-tidy'
    'pcre'
)
optdepends=(
    'php-pgsql: For postgres storage'
    'php-sqlite: For sqlite storage'
    'rabbitmq: For async import'
    'redis: For async import'
)
install="$pkgname.install"
options=(!strip)
source=("https://github.com/wallabag/wallabag/archive/${pkgver}.tar.gz")
#source=("${pkgname}-release-${pkgver}.tar.gz::http://wllbg.org/latest-v2-package") # you may try this URL, if the above one is not available
sha256sums=('0a6c954aee28d3b5246b0a829f43a643fdad3a3efc9d21683199a0626ed9ffe3')
backup=("etc/webapps/${pkgname}/parameters.yml"
        "usr/share/webapps/${pkgname}/parameters.yml"
        "var/lib/${pkgname}/data/db/wallabag.sqlite"
        "usr/share/webapps/${pkgname}/data/db/wallabag.sqlite")

package() {
    cd "${pkgdir}"
    mkdir -p usr/share/webapps
    mv "${srcdir}/${pkgname}-${pkgver}" usr/share/webapps/${pkgname}

    WALLABAG_CONF_DIR="${pkgdir}/usr/share/webapps/${pkgname}/app/config"

    install -d "${pkgdir}/etc/webapps/${pkgname}/"
    mv "${WALLABAG_CONF_DIR}"/parameters.yml.dist ${pkgdir}/etc/webapps/${pkgname}/parameters.yml
    chown -R http:http ${pkgdir}/etc/webapps/${pkgname}
    ln -s /etc/webapps/${pkgname}/parameters.yml "${WALLABAG_CONF_DIR}"/

    _VAR_DIR="${pkgdir}/var/lib/${pkgname}/"
    install -d "$_VAR_DIR"
    mv "${pkgdir}/usr/share/webapps/${pkgname}/"{data,var} "$_VAR_DIR"
    ln -s "/var/lib/${pkgname}/"{data,var} "${pkgdir}/usr/share/webapps/${pkgname}/"
    chown -R http:http "$_VAR_DIR" "${pkgdir}/usr/share/webapps/${pkgname}"
}
