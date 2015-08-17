# Maintainer: Your Name <youremail@domain.com>
pkgname=vim-ycm-patch
pkgver=7.4
pkgrel=1
pkgdesc="Vim with patch to remove annoying \"Pattern not found\" message when using YouCompleteMe plugin."
arch=('x86_64')
url="https://vim.org/"
license=('custom:vim')
makedepends=('mercurial' 'python' 'python2')
conflicts=('vim' 'gvim' 'vim-runtime' 'vi')
provides=('vim' 'gvim' 'vim-runtime')
source=('pum-silent.diff'
	'gvim.install'
	'gvim.desktop'
	'vim::hg+https://vim.googlecode.com/hg/')
md5sums=('8dc7425d62093f6a883feced883a3397'
         'f7e1e2722c972f3420cfd69492c79073'
         'd90413bd21f400313a785bb4010120cd'
         'SKIP')

build() {
  cd "$srcdir/vim"

  ./configure --with-python-config-dir=/usr/lib/python2.7/config --enable-pythoninterp --with-python3-config-dir=/usr/lib/python3.4/config-3.4m --with-features=huge --prefix=/usr --enable-gui=gtk2
  patch -p1 < "${srcdir}/../pum-silent.diff"
  make
}

package() {
  cd "$srcdir/vim"

  install=gvim.install

  make DESTDIR="$pkgdir/" install
  install -Dm644 "${srcdir}"/gvim.desktop \
    "${pkgdir}"/usr/share/applications/gvim.desktop
  install -Dm644 runtime/vim48x48.png "${pkgdir}"/usr/share/pixmaps/gvim.png
}
