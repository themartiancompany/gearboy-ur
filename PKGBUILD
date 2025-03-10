# SPDX-License-Identifier: AGPL-3.0

#    ----------------------------------------------------------------------
#    Copyright © 2025  Pellegrino Prevete
#
#    All rights reserved
#    ----------------------------------------------------------------------
#
#    This program is free software: you can redistribute it and/or modify
#    it under the terms of the GNU Affero General Public License as published by
#    the Free Software Foundation, either version 3 of the License, or
#    (at your option) any later version.
#
#    This program is distributed in the hope that it will be useful,
#    but WITHOUT ANY WARRANTY; without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#    GNU Affero General Public License for more details.
#
#    You should have received a copy of the GNU Affero General Public License
#    along with this program.  If not, see <https://www.gnu.org/licenses/>.

# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete <pellegrinoprevete@gmail.com>
# Contributor: aquova <mail at aquova dot net>

_os="$( \
  uname \
    -o)"
_Pkg="Gearboy"
pkgname="gearboy"
pkgver=3.6.1
pkgrel=1
pkgdesc="Game Boy / Gameboy Color emulator"
_http="https://github.com"
_ns="drhelius"
url="${_http}/${_ns}/${_Pkg}"
arch=(
  "x86_64"
  'i686'
  'arm'
  'armv7l'
  'aarch64'
  'mips'
  'powerpc'
  'pentium4'
)
license=(
  "GPL3"
)
depends=(
  'glew'
  'gtk3'
  'sdl2'
)
makedepends=()
if [[ "${_os}" == "Android" ]]; then
  makedepends+=(
    "libglvnd-dev"
  )
fi
_icon_ns="kodi-game"
_icon_proj="game.libretro.gearboy"
_icon_url="${_http}/${_icon_ns}/${_icon_proj}"
_network="100"
_fs="0x69470b18f8b8b5f92b48f6199dcb147b4be96571"
_namespace="0x87003Bd6C074C713783df04f36517451fF34CBEf"
_icon_sum="aa56beff8154c0b05e159a383adb2783382a5606068f6c5c1e9168dfdb14b2b0"
_evmfs_icon_uri="evmfs://${_network}/${_fs}/${_namespace}/${_icon_sum}"
source=(
  "${url}/archive/refs/tags/${pkgver}.tar.gz"
  "${pkgname}.png::${_evmfs_icon_uri}"
  "${pkgname}.desktop"
)
sha256sums=(
  "f3775ce38c7b65a36f8a9cc783b22928d08ef13c3458b3cb0da45dab65cda82e"
  "${_icon_sum}"
  "5a80ce1059171c5f4c65bb32b223a6494b5695e8d589db1bef7bda295cb9eb63"
)

_usr_get() {
  local \
    _bin
  _bin="$( \
    dirname \
      "$(command \
           -v \
	   "env")")"
  dirname \
    "${_bin}"
}

build() {
  cd \
    "${srcdir}/${_Pkg}-${pkgver}/platforms/linux"
  make
}

package() {
  cd \
    "${srcdir}/${_Pkg}-${pkgver}"
  install \
    -dm755 \
    "${pkgdir}/usr/lib/${pkgname}"
  install \
    -Dm755 \
    "platforms/linux/${pkgname}" \
    "${pkgdir}/usr/lib/${pkgname}"
  install \
    -Dm644 \
    "platforms/gamecontrollerdb.txt" \
    "${pkgdir}/usr/lib/${pkgname}"
  install \
    -dm755 \
    "${pkgdir}/usr/bin"
  ln \
    -s \
    "$(_usr_get)/lib/${pkgname}/${pkgname}" \
    "${pkgdir}/usr/bin/${pkgname}"
  install \
    -dm755 \
    "${pkgdir}/usr/share/icons"
  install \
    -Dm644 \
    "${srcdir}/${pkgname}.png" \
    "${pkgdir}/usr/share/icons/${pkgname}.png"
  install \
    -Dm755 \
    "${srcdir}/${pkgname}.desktop" \
    "${pkgdir}/usr/share/applications/${pkgname}.desktop"
  install \
    -Dm644 \
    "LICENSE" \
    "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
