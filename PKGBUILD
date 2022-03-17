#!/bin/bash

# Disable various shellcheck rules that produce false positives in this file.
# Repository rules should be added to the .shellcheckrc file located in the
# repository root directory, see https://github.com/koalaman/shellcheck/wiki
# and https://archiv8.github.io for further information.
# shellcheck disable=SC2034,SC2154
# ToDo: Add files: User documentation
# ToDo: Add files: Tooling
# FixMe: Namcap warnings and errors
# FixMe: Icons

# Maintainer: Fabian Bornschein <fabiscafe-cat-mailbox-dog-org>
# Contributor: Ross Clark <contact@artisteducator.com>


pkgbase=czkawka
pkgname=("czkawka-cli" "czkawka-gui")
pkgver=4.0.1
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
_commit=4a202633eef7b6155628bbf7449c03cdf8308169 # tags/3.3.1^0
source=("${pkgbase}-${pkgver}.tar.gz::https://github.com/qarmin/${pkgbase}/archive/refs/tags/${pkgver}.tar.gz")
sha512sums=(
  "6cb26126aedfbd62c71ef8d9a5491531ab5c194c0e0e51961f5c3f656aaafb691fad5036bbbfb8dfa5c05a40960c33172c142390d12fa9795e476881c18bad88"
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
  depends=("bzip2")
  license=("MIT")

  install -Dm644 "${srcdir}/${pkgbase}-${pkgver}/LICENSE" \
        "${pkgdir}/usr/share/licenses/czkawka-cli/LICENSE"
  install -Dm755 "${srcdir}/${pkgbase}-${pkgver}/target/release/czkawka_cli" \
        "${pkgdir}/usr/bin/czkawka_cli"
}

package_czkawka-gui() {
  depends=("gtk3")
  license=("MIT")

  install -Dm644 "${srcdir}/${pkgbase}-${pkgver}/LICENSE" \
        "${pkgdir}/usr/share/licenses/czkawka-gui/LICENSE"
  install -Dm755 "${srcdir}/${pkgbase}-${pkgver}/target/release/czkawka_gui" \
        "${pkgdir}/usr/bin/czkawka_gui"
  install -Dm644 "${srcdir}/${pkgbase}-${pkgver}/data/com.github.qarmin.czkawka.desktop" \
        "${pkgdir}/usr/share/applications/com.github.qarmin.czkawka.desktop"
}
