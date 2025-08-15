pkgname=libadwaita-without-adwaita
pkgver=1.7.6
pkgrel=2
url="https://gnome.pages.gitlab.gnome.org/libadwaita"
pkgdesc='libadwaita; Includes a patch to not overwrite the system theme. Because the maintainer likely abandoned the pkg'
arch=('i686' 'x86_64' 'armv7h' 'armv6h' 'aarch64')
license=(LGPL-2.1-or-later)

provides=("libadwaita=${pkgver}" "libadwaita-1.so=0-64")
conflicts=('libadwaita')

source=(
  "${pkgname}::git+https://gitlab.gnome.org/GNOME/libadwaita.git"
  theming_patch.diff
)
sha256sums=(
  SKIP
  SKIP
)

depends=(appstream fribidi glib2 glibc graphene gtk4 pango)
makedepends=(git meson gi-docgen sassc gobject-introspection vala pkg-config patch cmake libsass gcc glib2-devel)

build() {
  cd "${srcdir}/${pkgname}"
  git checkout "${pkgver}"
  <"${srcdir}"/theming_patch.diff patch src/adw-style-manager.c
  meson setup build \
    --prefix=/usr \
    -Dexamples=false \
    -Dtests=false
  ninja -C build
}

package() {
  cd "${srcdir}/${pkgname}"
  DESTDIR="$pkgdir" ninja -C build install
}
