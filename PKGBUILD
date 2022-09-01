#!/bin/bash

# Based on the original packaging by Fabian Bornschein <fabiscafe-cat-mailbox-dog-org>

# Disable various shellcheck rules that produce false positives in this file.
# Repository rules should be added to the .shellcheckrc file located in the
# repository root directory, see https://github.com/koalaman/shellcheck/wiki
# and https://archiv8.github.io for further information.
# shellcheck disable=SC2034,SC2154
# ToDo: Add files: User documentation
# ToDo: Add files: Tooling
# FixMe: Namcap warnings and errors

# Maintainer: Ross Clark <https://github.com/Archiv8/czkawka/discussions>
# Contributor: Ross Clark <https://github.com/Archiv8/czkawka/discussions>

pkgbase=czkawka
pkgname=(
  "czkawka-cli"
  "czkawka-gui"
)
pkgver=5.0.2
pkgrel=1
pkgdesc="Multi functional app to find duplicates, empty folders, similar images etc."
url="https://github.com/qarmin/czkawka"
arch=("x86_64")
makedepends=(
  # Official Arch Linux repositories
  "cargo"
  "git"
  "gtk4"
  "libheif"
  "rust"
)
checkdepends=(
  "xorg-server-xvfb"
)
# _commit=4a202633eef7b6155628bbf7449c03cdf8308169 # tags/3.3.1^0
source=("${pkgbase}-${pkgver}.tar.gz::https://github.com/qarmin/${pkgbase}/archive/refs/tags/${pkgver}.tar.gz")
sha512sums=(
  "2a6068d8c93310010ddbddc8c5462ff68bdb109f23f1c06972d916089a4bf310f9c2c6773fb64ba4966c251764f4777ea544f40d3ef8664e2fee5723d61cd021"
)

# pkgver() {
#  cd ${srcdir}
#  git describe --tags | sed "s/-/+/g"
# }

build() {
  cd "${srcdir}/${pkgbase}-${pkgver}"

  cargo build --bin czkawka_cli --release --features heif

  cargo build --bin czkawka_gui --release --features heif
}

check() {
  cd "${srcdir}/${pkgbase}-${pkgver}"

  cargo test --bin czkawka_cli --release

  dbus-run-session xvfb-run -s '-nolisten local' \
    cargo test --bin czkawka_gui --release
}

package_czkawka-cli() {
  depends=(
    "bzip2"
    "libheif"
  )
  license=(
    "MIT"
  )
  pkgdesc+=" (CLI)"

  install -Dm644 "${srcdir}/${pkgbase}-${pkgver}/LICENSE" \
    "${pkgdir}/usr/share/licenses/czkawka-cli/LICENSE"

  install -Dm755 "${srcdir}/${pkgbase}-${pkgver}/target/release/czkawka_cli" \
    "${pkgdir}/usr/bin/czkawka_cli"
}


package_czkawka-gui() {
  depends=(
    "gtk4"
    "libheif"
  )
  license=(
    "MIT"
  )
  pkgdesc+=" (Desktop App)"

  install -Dm644 "${srcdir}/${pkgbase}-${pkgver}/LICENSE" \
    "${pkgdir}/usr/share/licenses/czkawka-gui/LICENSE"

  install -Dm755 "${srcdir}/${pkgbase}-${pkgver}/target/release/czkawka_gui" \
    "${pkgdir}/usr/bin/czkawka_gui"

  install -Dm644 "${srcdir}/${pkgbase}-${pkgver}/data/com.github.qarmin.czkawka.desktop" \
    "${pkgdir}/usr/share/applications/com.github.qarmin.czkawka.desktop"

  install -Dm644 "${srcdir}/${pkgbase}-${pkgver}/data/icons/com.github.qarmin.czkawka.svg" \
    "${pkgdir}/usr/share/icons/hicolor/scalable/apps/com.github.qarmin.czkawka.svg"

  install -Dm644 "${srcdir}/${pkgbase}-${pkgver}/data/icons/com.github.qarmin.czkawka.Devel.svg" \
    "${pkgdir}/usr/share/icons/hicolor/scalable/apps/com.github.qarmin.czkawka.Devel.svg"

  install -Dm644 "${srcdir}/${pkgbase}-${pkgver}/data/icons/com.github.qarmin.czkawka-symbolic.svg" \
    "${pkgdir}/usr/share/icons/hicolor/symbolic/apps/com.github.qarmin.czkawka-symbolic.svg"

  install -Dm644 "${srcdir}/${pkgbase}-${pkgver}/data/com.github.qarmin.czkawka.metainfo.xml" \
    "${pkgdir}/usr/share/metainfo/com.github.qarmin.czkawka.metainfo.xml"
}
