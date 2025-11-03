_pkgname=waypaper-engine
pkgname=$_pkgname-git
pkgver=r153.66e2ba3
pkgrel=1
pkgdesc="Wallpaper Engine for Wayland compositors"
arch=('x86_64' 'aarch64')
url="https://github.com/FlashOnFire/waypaper-engine"
license=('GPL3')
depends=('wayland'
         'ffmpeg'
         'libglvnd'
         'libxkbcommon'
         'webkit2gtk-4.1')
makedepends=('rust' 'cargo' 'git' 'pnpm')
source=("git+$url.git")
sha256sums=('SKIP')

build() {
  cd "$srcdir/$_pkgname"

  cargo build --bin waypaper_engine_daemon --release --locked
  cargo build --bin waypaper_engine_cli --release --locked
  cargo build --bin waypaper_engine_ui --release --locked
}

package() {
  cd "$srcdir/$_pkgname"

  install -Dm0755 "target/release/waypaper_engine_daemon" "$pkgdir/usr/bin/waypaper_engine_daemon"
  install -Dm0755 "target/release/waypaper_engine_cli" "$pkgdir/usr/bin/waypaper_engine_cli"
  install -Dm0755 "target/release/waypaper_engine_ui" "$pkgdir/usr/bin/waypaper_engine_ui"

  install -Dm0644 "packaging/assets/waypaper_engine.desktop" "$pkgdir/usr/share/applications/waypaper_engine.desktop"

  install -Dm0644 "packaging/assets/logo.png" "$pkgdir/usr/share/pixmaps/waypaper_engine.png"
  install -Dm0644 "LICENSE" "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

pkgver() {
  cd "$_pkgname"
  printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short=7 HEAD)"
}

