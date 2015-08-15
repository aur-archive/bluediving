# Contributor: Jens Pranaitis <jens@jenux.homelinux.org>
# Contributer: Dawid Wrobel <cromo@klej.net>
pkgname=bluediving
pkgver=0.9
pkgrel=1
pkgdesc="A Bluetooth penetration testing suite"
url="http://bluediving.sourceforge.net/"
license=('GPL')
arch=('i686')
depends=(bluez-utils sox obexftp readline expat perl-xml-simple)
makedepends=()
install=bluediving.install
source=(http://downloads.sourceforge.net/sourceforge/$pkgname/$pkgname-$pkgver.tgz)
build() {
md5sums=('53365a068e7e65a2b047b96998ad3f9d')

  cd "${srcdir}"/$pkgname-$pkgver
  # change the bluedivingNG.conf path to /etc
  sed -i -e 's/bluedivingNG.conf/\/etc\/bluedivingNG.conf/g' bluedivingNG.pl || exit 1
  # change the paths of the compiled tools to /usr/bin/
  sed -i -e 's/tools\//\/usr\/bin\//g' bluedivingNG.conf || exit 1
  # change the why-the-hell-am-I-having-such-a-long-name vcard path
  sed -i -e '/vcards\/AAAA/ c\  <vcard>/usr/share/bluediving/AAA.vcf</vcard>' bluedivingNG.conf || exit 1
  #change the sounds paths
  sed -i -e 's/sounds\//\/usr\/share\/bluediving\//g' bluedivingNG.conf || exit 1
  # fix libxml2 missing includes compilation error
  sed -i -e 's/gcc/gcc `xml2-config --cflags`/g' tools/btftp_src/Makefile || exit 1
  # fix bss directory path
  sed -i -e 's/bss-0.6/bss-0.8/g' tools/make_tools.sh || exit 1
  cd tools
  sh make_tools.sh || return 1

  mkdir -p "${pkgdir}"/usr/bin/

  install -m755 atshell attest bccmd bdaddr bss btobex btftp carwhisperer greenplaque \
	hcidump-crash hstest l2cap-packet l2cap_headersize_overflow redfang \
	rfcomm_shell hidattack "${pkgdir}"/usr/bin/ || return 1
  install -D -m755 "${srcdir}"/$pkgname-$pkgver/bluedivingNG.pl    "${pkgdir}"/usr/bin/bluedivingNG.pl || return 1
  install -D -m644 "${srcdir}"/$pkgname-$pkgver/bluedivingNG.conf  "${pkgdir}"/etc/bluedivingNG.conf || return 1
  install -D -m644 "${srcdir}"/$pkgname-$pkgver/vcards/AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA.vcf \
	   "${pkgdir}"/usr/share/bluediving/AAA.vcf || return 1
  install -D -m644 "${srcdir}"/$pkgname-$pkgver/sounds/explosion.wav "${pkgdir}"/usr/share/bluediving/explosion.wav || return 1
  install -D -m644 "${srcdir}"/$pkgname-$pkgver/tools/carwhisperer-0.2/out.raw "${pkgdir}"/usr/share/bluediving/out.raw || return 1
}
md5sums=('53365a068e7e65a2b047b96998ad3f9d')
