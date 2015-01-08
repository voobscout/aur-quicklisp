# Maintainer: Voobscout <voobscout+aur@gmail.com>

pkgname=quicklisp
pkgver=17122014
pkgrel=1
pkgdesc="Quicklisp is a library manager for Common Lisp."
arch=('i686' 'x86_64')
license=('GPL2')
depends=('sbcl')
makedepends=('git' 'texinfo' 'autoconf')
url="http://www.quicklisp.org"
provides=('quicklisp')
conflicts=('lispbox')
source=('http://beta.quicklisp.org/quicklisp.lisp'
        'sbclrc'
       )
sha256sums=('47cfdc0f4796b4c0ca05af16b666dd4b21c5b9e62b731390c895c2d19ed6d095'
            '4215c0f202a14866023ccc6f9b18f57682ca8295473a062bbe15de4d1a53b5e8')

install=quicklisp.install
options=(!strip)  # Thanks to sidereus for pointing this out

build() {
  msg "Installing quicklisp..."
  curl -O http://beta.quicklisp.org/quicklisp.lisp

  sbcl --load ${srcdir}/quicklisp.lisp \
       --non-interactive \
       --eval "(quicklisp-quickstart:install :path \"${srcdir}/quicklisp-install\")" \
       --eval "(ql:update-client)" \
       --eval "(ql:update-all-dists)"
}

package() {
  msg "Installing /etc/sbclrc"
  install -Dm 644 ${srcdir}/sbclrc ${pkgdir}/etc/sbclrc

  msg "Installing quicklisp"
  install -d ${pkgdir}/usr/share/common-lisp/source/quicklisp
  install -m 0644 ${srcdir}/quicklisp-install/*.lisp ${pkgdir}/usr/share/common-lisp/source/quicklisp
  install -m 0644 ${srcdir}/quicklisp-install/*.sexp ${pkgdir}/usr/share/common-lisp/source/quicklisp

  install -m 0777 -d ${pkgdir}/usr/share/common-lisp/source/quicklisp/dists/quicklisp
  install -m 0644 ${srcdir}/quicklisp-install/dists/quicklisp/*.txt ${pkgdir}/usr/share/common-lisp/source/quicklisp/dists/quicklisp

  install -m 0777 -d ${pkgdir}/usr/share/common-lisp/source/quicklisp/local-projects

  install -d ${pkgdir}/usr/share/common-lisp/source/quicklisp/quicklisp
  install -m 0644 ${srcdir}/quicklisp-install/quicklisp/*.* ${pkgdir}/usr/share/common-lisp/source/quicklisp/quicklisp

  install -m 0777 -d ${pkgdir}/usr/share/common-lisp/source/quicklisp/cache
  install -m 0777 -d ${pkgdir}/usr/share/common-lisp/source/quicklisp/tmp
 }
