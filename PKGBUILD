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

# Maintainer:
#   Truocolo
#     <truocolo@aol.com>
#     <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
# Maintainer:
#   Pellegrino Prevete (dvorak)
#     <pellegrinoprevete@gmail.com>
#     <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
# Maintainer:
#   Tomislav Ivek
#     <tomislav dot ivek at gmail dot com>

_evmfs_available="$( \
  command \
    -v \
    "evmfs" || \
    true)"
if [[ ! -v "_evmfs" ]]; then
  if [[ "${_evmfs_available}" != "" ]]; then
    _evmfs="true"
  elif [[ "${_evmfs_available}" == "" ]]; then
    _evmfs="false"
  fi
fi
_py="python"
_pyver="$( \
  "${_py}" \
    -V | \
    awk \
      '{print $2}')"
_pymajver="${_pyver%.*}"
_pyminver="${_pymajver#*.}"
_pynextver="${_pymajver%.*}.$(( \
  ${_pyminver} + 1))"
_pkg=patch-ng
pkgname="${_py}-${_pkg}"
pkgver=1.18.0
pkgrel=2
_pkgdesc=(
  "Library to parse and apply"
  "unified diffs forked from"
  "python-patch."
)
pkgdesc="${_pkgdesc[*]}"
arch=(
  'any'
)
_http="https://github.com"
_ns="conan-io"
url="${_http}/${_ns}/${pkgname}"
license=(
  'MIT'
)
depends=(
  "${_py}>=${_pymajver}"
  "${_py}<${_pynextver}"
)
makedepends=(
  "${_py}-setuptools"
)
_name="${_pkg}"
_tarname="${_pkg}-${pkgver}"
_evmfs_network="100"
_evmfs_address="0x69470b18f8b8b5f92b48f6199dcb147b4be96571"
_evmfs_ns="0x87003Bd6C074C713783df04f36517451fF34CBEf"
_archive_sum="da067628d6d5fd9dc5a55eab37951d46bd95661b7219fab364b711366abcc690"
_evmfs_archive_uri="evmfs://${_evmfs_network}/${_evmfs_address}/${_evmfs_ns}/${_archive_sum}"
_evmfs_archive_src="${_tarname}.zip::${_evmfs_archive_uri}"
_archive_sig_sum="02c5e6b675f09a44674ffb9ddd1035ad1fcd3268f6eda6646817ad3e9de51d00"
_archive_sig_uri="evmfs://${_evmfs_network}/${_evmfs_address}/${_evmfs_ns}/${_archive_sig_sum}"
_archive_sig_src="${_tarname}.zip.sig::${_archive_sig_uri}"
if [[ "${_evmfs}" == "true" ]]; then
  makedepends+=(
    "evmfs"
  )
  _src="${_evmfs_archive_src}"
  source+=(
    "${_archive_sig_src}"
  )
  sha256sums+=(
    "${_archive_sig_sum}"
  )
if [[ "${_evmfs}" == "false" ]];then
  _pypa="https://pypi.io/packages/source"
  _uri="${_pypa}/${_pkg::1}/${_pkg}/${_tarname}.tar.gz"
  _src="${pkgname}-${pkgver}.tar.gz::${_uri}"
fi

fi
source=(
  "${_src}"
  # "https://raw.githubusercontent.com/${_ns}/${pkgname}/${pkgver}/LICENSE"
)
sha256sums=(
  "${_archive_sum}"
)
md5sums=(
  '5df1f6f28b8fcf09bc4dfd182caa12d8'
)
validpgpkeys=(
  # Pellegrino Prevete (dvorak)
  #   <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
  '12D8E3D7888F741E89F86EE0FEC8567A644F1D16'
)

build() {
  cd \
    "${srcdir}/${_tarname}"
  "${_py}" \
    "setup.py" \
      build
}

package() {
  cd \
    "${srcdir}/${_tarname}"
  "${_py}" \
    "setup.py" \
      install \
        --optimize=1 \
	--root="${pkgdir}"
  # install \
  #   -vDm644 \
  #   "LICENSE" \
  #   "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
