# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Pellegrino Prevete <pellegrinoprevete@gmail.com>
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: George Rawlinson <grawlinson@archlinux.org>
# Contributor: Felix Yan <felixonmars@archlinux.org>
# Contributor: Daniel Wallace <danielwallace at gtmanfred.com>
# Contributor: Bogdan Szczurek <thebodzio@gmail.com>
# Contributor: Ismo Toijala <ismo.toijala@gmail.com>

_py="python"
_pkg="jsonschema"
pkgname="${_py}-${_pkg}"
pkgver=4.22.0
pkgrel=1
pkgdesc='An implementation of JSON Schema validation for Python'
arch=(
  'any'
)
_http="https://github.com"
_ns="${pkgname}"
url="${_http}/${pkgname}/${_pkg}"
license=(
  'MIT'
)
depends=(
  "${_py}"
  "${_py}-attrs"
  "${_py}-pyrsistent"
  "${_py}-referencing"
  "${_py}-jsonschema-specifications"
)
makedepends=(
  'git'
  "${_py}-build"
  "${_py}-installer"
  "${_py}-wheel"
  "${_py}-hatchling"
  "${_py}-hatch-vcs"
  "${_py}-hatch-fancy-pypi-readme"
)
checkdepends=(
  "${_py}-pip"
  "${_py}-twisted"
  "${_py}-isoduration"
  "${_py}-fqdn"
  "${_py}-idna"
  "${_py}-jsonpointer"
  "${_py}-rfc3339-validator"
  "${_py}-rfc3987"
  "${_py}-uri-template"
  "${_py}-webcolors"
)
optdepends=(
  "${_py}-isoduration: for duration format"
  "${_py}-fqdn: for hostname format"
  "${_py}-idna: for idn-hostname format"
  "${_py}-jsonpointer: for json-pointer & relative-json-pointer format"
  "${_py}-rfc3339-validator: for date-time format"
  "${_py}-rfc3987: for iri, iri-reference, uri & uri-reference format"
  "${_py}-uri-template: for uri-template format"
  "${_py}-webcolors: for color format"
)
source=(
  "${pkgname}::git+${url}#tag=v${pkgver}"
)
sha512sums=(
  '7eff6dc0967af8d0a75a2f288410bbc8ef597fa4f4479bf47663ffd9342f6791c87c1de75bf761a7fea3b13fb603196871dbd49f715001ebff7a3671b044b682'
)
b2sums=(
  'e3810424e3a6c61b7f22bbb25abc7dd1497c36c87398fb4befbd4f706b791ed2fe0a27fd81b7aeded2aadc55bca50a7cde8ae6321f8678a8341fc5ac47b61cd6'
)

build() {
  cd \
    "${pkgname}"
  "${_py}" \
    -m build \
    --wheel \
    --no-isolation
}

check() {
  local \
    site_packages
  cd \
    "${pkgname}"
  site_packages="$( \
      "${_py}" \
        -c \
	"import site; print(site.getsitepackages()[0])")"
  # install to temporary directory
  "${_py}" \
    -m \
      installer \
    --destdir="$PWD/tmp_install" \
    dist/*.whl
  PYTHONPATH="$PWD/tmp_install$site_packages" \
  JSON_SCHEMA_TEST_SUITE=json \
  trial \
    jsonschema
}

package() {
  local \
    _site_packages
  _site_packages="$( \
    "${_py}" \
      -c \
        "import site; print(site.getsitepackages()[0])")"
  "${_py}" \
    -m installer \
    --destdir="${pkgdir}" \
    dist/*.whl
  # symlink license file
  install \
    -d "${pkgdir}/usr/share/licenses/${pkgname}"
  ln \
    -s \
    "${_site_packages}/${_pkg}-${pkgver}.dist-info/licenses/COPYING" \
    "${pkgdir}/usr/share/licenses/${pkgname}/COPYING"
}

# vim:set sw=2 sts=-1 et:
