# Maintainer: Maxwell Pray a.k.a. Synthead <synthead@gmail.com>
# Contributor: Justin Davis <jrcd83@gmail.com>

_cpanname="namespace-clean"
pkgname="perl-$_cpanname"
pkgver="0.25"
pkgrel="1"
pkgdesc="Keep imports and functions out of your namespace"
arch=("any")
license=("PerlArtistic" "GPL")
options=("!emptydirs")
depends=("perl>=5.5.0" "perl-b-hooks-endofscope>=0.12" "perl-package-stash>=0.23")
url="http://search.cpan.org/dist/$_cpanname"
source=("http://search.cpan.org/CPAN/authors/id/R/RI/RIBASUSHI/$_cpanname-$pkgver.tar.gz")
sha1sums=('a76713df74b2b865ffed31603e1a1fae544c3026')

# Function to change to the working directory and set
# environment variables to override undesired options.
prepareEnvironment() {
	cd "$srcdir/$_cpanname-$pkgver"
	export \
		PERL_MM_USE_DEFAULT=1 \
		PERL_AUTOINSTALL=--skipdeps \
		PERL_MM_OPT="INSTALLDIRS=vendor DESTDIR='$pkgdir'" \
		PERL_MB_OPT="--installdirs vendor --destdir '$pkgdir'" \
		MODULEBUILDRC=/dev/null
}

build() {
	prepareEnvironment
	/usr/bin/perl Makefile.PL
	make
}

check() {
	prepareEnvironment
	make test
}

package() {
	prepareEnvironment
	make install

	# Remove "perllocal.pod" and ".packlist".
	find "$pkgdir" -name .packlist -o -name perllocal.pod -delete
}
