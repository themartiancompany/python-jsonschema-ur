# Maintainer: Daniel Wallace <danielwallace at gtmanfred.com>
# Contributor: Bogdan Szczurek <thebodzio@gmail.com>
# Contributor: Ismo Toijala <ismo.toijala@gmail.com>

pkgbase=python-jsonschema
_pkgname=jsonschema
pkgname=(python-jsonschema python2-jsonschema)
pkgver=2.6.0
pkgrel=1
pkgdesc="An implementation of JSON Schema validation for Python"
arch=(any)
url="http://pypi.python.org/pypi/jsonschema"
license=('MIT')
makedepends=(python-setuptools python2-setuptools)
source=("https://pypi.io/packages/source/j/jsonschema/${pkgname:7}-$pkgver.tar.gz")
md5sums=('50c6b69a373a8b55ff1e0ec6e78f13f4')

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
  depends=(python2-functools32)
  install -D -m644 json/LICENSE $pkgdir/usr/share/licenses/$pkgname/LICENSE
  mv $pkgdir/usr/bin/jsonschema{,2}
}

