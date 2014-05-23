# Maintainer: Daniel Wallace <danielwallace at gtmanfred.com>
# Contributor: Bogdan Szczurek <thebodzio@gmail.com>
# Contributor: Ismo Toijala <ismo.toijala@gmail.com>

pkgbase=python-jsonschema
_pkgname=jsonschema
pkgname=(python-jsonschema python2-jsonschema)
pkgver=2.3.0
pkgrel=3
pkgdesc="An implementation of JSON Schema validation for Python"
arch=(any)
url="http://pypi.python.org/pypi/jsonschema"
license=('MIT')
makedepends=(python-setuptools python2-setuptools)
source=("http://pypi.python.org/packages/source/j/jsonschema/${pkgname:7}-$pkgver.tar.gz")

prepare(){
    cp -a $_pkgname-$pkgver $_pkgname-$pkgver-2
    find $_pkgname-$pkgver-2 -name \*.py -exec sed -i '1s/python$/&2/' {} +
}

package_python-jsonschema() {
  cd "$srcdir/$_pkgname-$pkgver"
  python setup.py install --root="$pkgdir/" --optimize=1
  depends=(python)
  install -D -m644 json/LICENSE $pkgdir/usr/share/licenses/$pkgname/LICENSE
}

package_python2-jsonschema() {
  cd "$srcdir/$_pkgname-$pkgver-2"
  python2 setup.py install --root="$pkgdir/" --optimize=1
  depends=(python2)
  install -D -m644 json/LICENSE $pkgdir/usr/share/licenses/$pkgname/LICENSE
}

md5sums=('410075e1969a9ec1838b5a6e1313c32b')
