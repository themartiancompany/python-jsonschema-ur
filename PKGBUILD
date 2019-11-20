# Maintainer: Felix Yan <felixonmars@archlinux.org>
# Contributor: Daniel Wallace <danielwallace at gtmanfred.com>
# Contributor: Bogdan Szczurek <thebodzio@gmail.com>
# Contributor: Ismo Toijala <ismo.toijala@gmail.com>

pkgbase=python-jsonschema
pkgname=('python-jsonschema' 'python2-jsonschema')
pkgver=3.2.0
pkgrel=1
pkgdesc="An implementation of JSON Schema validation for Python"
arch=('any')
url="https://pypi.python.org/pypi/jsonschema"
license=('MIT')
makedepends=('python-attrs' 'python2-attrs' 'python-importlib-metadata' 'python2-importlib-metadata'
             'python-pyrsistent' 'python2-pyrsistent' 'python2-functools32' 'python-setuptools-scm'
             'python2-setuptools-scm')
checkdepends=('python-twisted' 'python2-twisted' 'python-idna' 'python2-idna' 'python-jsonpointer'
              'python2-jsonpointer' 'python-strict-rfc3339' 'python2-strict-rfc3339'
              'python-rfc3987' 'python2-rfc3987' 'python-webcolors' 'python2-webcolors')
source=("$pkgbase-$pkgver.tar.bz2::https://github.com/Julian/jsonschema/archive/v$pkgver.tar.gz")
sha512sums=('a575e9e7b0668220854e7ae45f2afd433643c3f0bfeb9769413cfc072ae01513a8d97bddbb6317f42348e09081e72bbad801d00ee5e3c0ac840bd19e934955cd')

export SETUPTOOLS_SCM_PRETEND_VERSION=$pkgver

prepare() {
  cp -a jsonschema-$pkgver{,-py2}
  find jsonschema-$pkgver-py2 -name \*.py -exec sed -i '1s/python$/&2/' {} +
}

build() {
  cd "$srcdir"/jsonschema-$pkgver
  python setup.py build

  cd "$srcdir"/jsonschema-$pkgver-py2
  python2 setup.py build
}

check() {
  cd "$srcdir"/jsonschema-$pkgver
  python setup.py install --root="$PWD/tmp_install" --optimize=1
  PYTHONPATH="$PWD/tmp_install/usr/lib/python3.8/site-packages" JSON_SCHEMA_TEST_SUITE=json trial3 jsonschema
  python -m doctest README.rst

  cd "$srcdir"/jsonschema-$pkgver-py2
  python2 setup.py install --root="$PWD/tmp_install" --optimize=1
  PYTHONPATH="$PWD/tmp_install/usr/lib/python2.7/site-packages" JSON_SCHEMA_TEST_SUITE=json trial jsonschema
  python2 -m doctest README.rst
}

package_python-jsonschema() {
  depends=('python-attrs' 'python-importlib-metadata' 'python-pyrsistent' 'python-setuptools')

  cd jsonschema-$pkgver
  python setup.py install --root="$pkgdir" --optimize=1
  install -D -m644 json/LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}

package_python2-jsonschema() {
  depends=('python2-attrs' 'python2-importlib-metadata' 'python2-pyrsistent' 'python2-setuptools'
           'python2-functools32')

  cd jsonschema-$pkgver-py2
  python2 setup.py install --root="$pkgdir" --optimize=1
  install -D -m644 json/LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE

  mv "$pkgdir"/usr/bin/jsonschema{,2}
}

