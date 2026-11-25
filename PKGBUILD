
# Maintainer: YOUR NAME <YOUR EMAIL>

pkgname=samovar-lite
pkgver=1.0.0
pkgrel=2
pkgdesc="PotPlayer-style media player for Linux, built on libmpv and Qt"
arch=('any')
url="https://github.com/AliMilani/samovar-lite"
license=('GPL-3.0-or-later')

depends=(
  'python'
  'pyside6'
  'python-mpv'
  'mpv'
)

makedepends=(
  'python-build'
  'python-installer'
  'python-hatchling'
)

source=(
  "$pkgname-$pkgver.tar.gz::https://github.com/AliMilani/samovar-lite/archive/refs/tags/v$pkgver.tar.gz"
)

sha256sums=(
  'f687a1063b62eec017b6a2411ddef1466628c2963ecb1ed1eb52970e5771b2ea'
)

build() {
  cd "$srcdir/$pkgname-$pkgver"
  python -m build --wheel --no-isolation
}

package() {
  cd "$srcdir/$pkgname-$pkgver"

  # Install Python application
  python -m installer --destdir="$pkgdir" dist/*.whl

  # Install license
  install -Dm644 LICENSE \
    "$pkgdir/usr/share/licenses/$pkgname/LICENSE"

  # Install application icon
  install -Dm644 docs/images/icon.png \
    "$pkgdir/usr/share/icons/hicolor/256x256/apps/samovar-lite.png"

  # Install desktop entry
  install -d "$pkgdir/usr/share/applications"

  cat > "$pkgdir/usr/share/applications/samovar-lite.desktop" <<'EOF'
[Desktop Entry]
Name=Samovar Lite
Comment=PotPlayer-style media player for Linux
Exec=samovar-lite %F
Icon=samovar-lite
Terminal=false
Type=Application
Categories=AudioVideo;Player;
StartupNotify=true
EOF
}

