# Maintainer: Marcel Huber <`echo "moc tknup liamg tä oofrebuhlecram" | rev`>
_perlmod=ora2pg
pkgname=perl-$_perlmod
pkgver=13.0.3.g2310354
pkgrel=1
pkgdesc="Oracle to PostgreSQL database schema converter"
arch=('any')
url="http://ora2pg.darold.net/"
license=('GPL')
depends=('perl>=5.10.0')
makedepends=()
options=(!emptydirs)
install=
source=("$pkgname"::'git+git://github.com/darold/ora2pg.git')
sha256sums=('SKIP')

pkgver() {
  cd "$srcdir/$pkgname"
  if GITTAG="$(git describe --abbrev=0 --tags 2>/dev/null)"; then
    local _revs_ahead_tag=$(git rev-list --count ${GITTAG}..)
    local _commit_id_short=$(git log -1 --format=%h)
    echo $(sed -e s/^${pkgname%%-git}// -e 's/^[-_/a-zA-Z]\+//' -e 's/[-_+]/./g' <<< ${GITTAG}).${_revs_ahead_tag}.g${_commit_id_short}
  else
    echo 0.$(git rev-list --count master).g$(git log -1 --format=%h)
  fi
}

build() {
  cd "$srcdir/$pkgname"

  # Install module in vendor directories.
  PERL_MM_USE_DEFAULT=1 perl Makefile.PL INSTALLDIRS=vendor
  make
}

package() {
  cd "$srcdir/$pkgname"
  make install DESTDIR="$pkgdir/"
}

# vim:set ts=2 sw=2 et:
