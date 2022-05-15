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
pkgver=4.1.0
pkgrel=1
pkgdesc="Multi functional app to find duplicates, empty folders, similar images etc."
url="https://github.com/qarmin/czkawka"
arch=("x86_64")
makedepends=(
  # Official Arch Linux repositories
  "cargo"
  "git"
  "gtk3"
  "rust"
)
# _commit=4a202633eef7b6155628bbf7449c03cdf8308169 # tags/3.3.1^0
source=("${pkgbase}-${pkgver}.tar.gz::https://github.com/qarmin/${pkgbase}/archive/refs/tags/${pkgver}.tar.gz")
sha512sums=(
  "7bba7f7b4cfb60d4ab44d45edfd0594ac18372b91b2935e80c2da05a44c72e9d4d455552f161ab6fc078682743ba0c0b2a66792f4141c0c64550f6da7f66cb12"
)

# pkgver() {
#  cd ${srcdir}
#  git describe --tags | sed "s/-/+/g"
# }

build() {
  cd ${srcdir}/${pkgbase}-${pkgver}
  cargo build --bin czkawka_cli --release
  cargo build --bin czkawka_gui --release
}

check() {
  cd ${srcdir}/${pkgbase}-${pkgver}
  cargo test --bin czkawka_cli --release
  cargo test --bin czkawka_gui --release
}

package_czkawka-cli() {
  depends=(
    "bzip2"
  )
  license=(
    "MIT"
  )

  install -Dm644 "${srcdir}/${pkgbase}-${pkgver}/LICENSE" \
    "${pkgdir}/usr/share/licenses/czkawka-cli/LICENSE"
  install -Dm755 "${srcdir}/${pkgbase}-${pkgver}/target/release/czkawka_cli" \
    "${pkgdir}/usr/bin/czkawka_cli"
}

package_czkawka-gui() {
  depends=(
    "gtk3"
  )
  license=(
    "MIT"
  )

  install -Dm644 "${srcdir}/${pkgbase}-${pkgver}/LICENSE" \
    "${pkgdir}/usr/share/licenses/czkawka-gui/LICENSE"
  install -Dm755 "${srcdir}/${pkgbase}-${pkgver}/target/release/czkawka_gui" \
    "${pkgdir}/usr/bin/czkawka_gui"
  install -Dm644 "${srcdir}/${pkgbase}-${pkgver}/data/com.github.qarmin.czkawka.desktop" \
    "${pkgdir}/usr/share/applications/com.github.qarmin.czkawka.desktop"
}
