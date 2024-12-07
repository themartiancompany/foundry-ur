# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Oliver Nordbjerg <hi@notbjerg.me>

_os="$( \
  uname \
    -o)"
_pkg=foundry
pkgname="${_pkg}"
# pkgver=1.0.0
pkgver="2024.12.06"
_commit="00efa0d5965269149f374ba142fb1c3c7edd6c94"
pkgrel=1
_pkgdesc=(
  "A blazing fast, portable and modular"
  "toolkit for Ethereum application"
  "development written in Rust."
)
pkgdesc="${_pkgdesc[*]}"
arch=(
  'x86_64'
  'aarch64'
  'arm'
  'armv7l'
  'armv6l'
  'mips'
  'powerpc'
  'pentium4'
  'i686'
)
url="https://get${_pkg}.sh"
license=(
  'MIT'
  'APACHE'
)
depends=(
  libusb
)
makedepends=(
  'git'
  'cargo'
)
provides=(
  'forge'
  'cast'
  'anvil'
  'chisel'
)
_http="https://github.com"
_ns="${_pkg}-rs"
_url="${_http}/${_ns}/${_pkg}"
# _tag_name="tag"
# _tag="v${pkgver}"
_tag_name="commit"
_tag="${_commit}"
_tarname="${_pkg}-${_tag}"
_src="${_tarname}::git+${_url}.git#${_tag_name}=${_tag}"
source=(
  "${_src}"
)
sha512sums=(
  'SKIP'
)

_target_get() {
  local \
    _target 
  _target="${CARCH}-unknown-linux-gnu"
  if [[ "${_os}" == "Android" ]]; then
    _target="${CARCH}-linux-androideabi"
  fi
  echo \
    "${_target}"
}

prepare() {
  local \
    _target
  _target="$( \
    _target_get)"
  cd \
    "${_tarname}"
  export \
    RUSTUP_TOOLCHAIN=stable
  cargo \
    fetch \
      --locked \
      --target \
        "${_target}"
}

build() {
  cd \
    "${_tarname}"
  export \
    RUSTUP_TOOLCHAIN=stable
  export \
    CARGO_TARGET_DIR=target
  cargo \
    build \
      --bins \
      --frozen \
      --release
}

package() {
  cd \
    "${_tarname}"
  install \
    -Dm755 \
    "target/release/forge" \
    "${pkgdir}/usr/bin/forge"
  install \
    -Dm755 \
    "target/release/cast" \
    "${pkgdir}/usr/bin/cast"
  install \
    -Dm755 \
    "target/release/anvil" \
    "${pkgdir}/usr/bin/anvil"
  install \
    -Dm755 \
    "target/release/chisel" \
    "${pkgdir}/usr/bin/chisel"
  install \
    -Dm644 \
    "LICENSE-MIT" \
    "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE-MIT"
  install \
    -Dm644 \
    "LICENSE-APACHE" \
    "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE-APACHE"
}
