# Maintainer: Det <nimetonmaili at gmail a-dot com>
# Contributor: Simon Tunnat <simon+aur@tunn.at>
# Based on thunderbird-beta-bin: https://aur.archlinux.org/packages/thunderbird-beta-bin/

pkgname=thunderbird-esr-bin
pkgver=17.0.11
pkgrel=1
pkgdesc="Standalone Mail/News reader - Extended Support Release"
arch=('i686' 'x86_64')
url="https://www.mozilla.org/thunderbird/organizations"
license=('GPL' 'LGPL' 'MPL')
depends=('alsa-lib' 'cairo' 'dbus-glib' 'desktop-file-utils' 'fontconfig' 'freetype2' 'gtk-update-icon-cache'
         'gtk2' 'hicolor-icon-theme' 'hunspell' 'libnotify' 'libpng' 'libvpx' 'libxt' 'mime-types'
         'mozilla-common' 'nss' 'pixman' 'sqlite' 'startup-notification')
optdepends=('libcanberra: for sound support')
provides=("thunderbird=$pkgver")
install=$pkgname.install
_arch=i686  # Workaround for the AUR Web interface Source parser
[ "$CARCH" = 'x86_64' ] && _arch=x86_64
source=("https://ftp.mozilla.org/pub/mozilla.org/thunderbird/releases/${pkgver}esr/linux-$_arch/en-US/thunderbird-${pkgver}esr.tar.bz2"
        'thunderbird-esr.desktop'
        'vendor.js')
# # Alternative mirror:
# source[0]="http://releases.mozilla.org/pub/mozilla.org/thunderbird/releases/${pkgver}esr/linux-$_arch/en-US/thunderbird-${pkgver}esr.tar.bz2"
md5sums=(`curl -sL ${source/\/li*}/MD5SUMS | sed -nr "s/(.*) .*$CARCH".*en-US.*bz2/\1/p`
         'c4162b713e9d063202a079d2243fdc93'
         '90264419778975f57d74696ac2ad7107')

package() {
  msg2 "Creating directories"
  # Create directories
  install -d "$pkgdir"/{usr/bin,opt}

  msg2 "Moving stuff in place"
  # Install
  cp -r thunderbird/ "$pkgdir"/opt/thunderbird-esr-$pkgver/
  cp vendor.js "$pkgdir"/opt/thunderbird-esr-$pkgver/defaults/pref/
  
  # /usr/bin symlink
  ln -s /opt/thunderbird-esr-$pkgver/thunderbird "$pkgdir"/usr/bin/thunderbird-esr
  
  # Icons
  for i in 16x16 22x22 24x24 32x32 48x48 256x256; do
    install -Dm644 thunderbird/chrome/icons/default/default${i/x*/}.png "$pkgdir"/usr/share/icons/hicolor/$i/apps/thunderbird-esr.png
  done
  
  # Desktop
  install -Dm644 thunderbird-esr.desktop "$pkgdir"/usr/share/applications/thunderbird-esr.desktop
  
  # Dictionaries
  rm -rf "$pkgdir"/opt/thunderbird-esr-$pkgver/dictionaries/
  ln -sf /usr/share/hunspell/ "$pkgdir"/opt/thunderbird-esr-$pkgver/dictionaries
  
  # Hyphenation
  ln -sf /usr/share/hyphen/ "$pkgdir"/opt/thunderbird-esr-$pkgver/hyphenation
}