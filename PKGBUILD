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
source=(
  "${url}/archive/refs/tags/${pkgver}.tar.gz"
)
sha256sums=(
  "f3775ce38c7b65a36f8a9cc783b22928d08ef13c3458b3cb0da45dab65cda82e"
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
    "${srcdir}/${_Pkg}-${pkgver}/platforms/linux"
  mkdir \
    -p \
    "${pkgdir}/opt/gearboy"
  install \
    -Dm755 \
    "linux/${pkgname}" \
    "${pkgdir}/usr/lib/${pkgname}"
  install \
    -Dm644 \
    "gamecontrollerdb.txt" \
    "${pkgdir}/usr/lib/${pkgname}"
  install \
    -dm755 \
    "${pkgdir}/usr/bin"
  ln \
    -s \
    "$(_usr_get)/lib/${pkgname}/${pkgname}" \
    "${pkgdir}/usr/bin/${pkgname}"
  install \
    -Dm644 \
    "LICENCE" \
    "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
