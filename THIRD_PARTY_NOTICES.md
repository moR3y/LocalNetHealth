# LocalNetHealth Third-Party Notices

This inventory is based on the final Windows installer payload, expanded
locally from `LocalNetHealth-1.0.0.exe`. It covers application packages and
the native/runtime components that are actually present in the bundled
Python runtime. The application source uses Python standard-library modules
and is not included in the public distribution staging.

## Python packages

| Component | Exact version | Bundled path | License identifier | License text / obligations |
| --- | --- | --- | --- | --- |
| Python runtime | 3.12.13 | `runtime_env/python` | Python Software Foundation License 2.0 | `runtime_env/python/LICENSE.txt`; retain notices and comply with the Windows binary redistribution conditions in that file |
| Pillow | 12.2.0 | `runtime_env/python/Lib/site-packages/PIL` and `pillow-12.2.0.dist-info` | MIT-CMU | `.dist-info/METADATA` and `.dist-info/licenses/LICENSE`; retain copyright and license notice |
| pystray | 0.19.5 | `runtime_env/python/Lib/site-packages/pystray` and `pystray-0.19.5.dist-info` | LGPL-3.0 | `.dist-info/METADATA`, `COPYING`, and `COPYING.LGPL`; preserve LGPL notice and allow replacement/relinking as required by LGPL-3.0 |
| six | 1.17.0 | `runtime_env/python/Lib/site-packages/six.py` and `six-1.17.0.dist-info` | MIT | `.dist-info/METADATA` and `.dist-info/LICENSE`; retain copyright and license notice |
| pywin32 | 312 | `runtime_env/python/Lib/site-packages/win32*`, `pythonwin`, `pywin32_system32`, and `pywin32-312.dist-info` | PSF / component-specific notices | `.dist-info/METADATA`, `.dist-info/licenses/*`, `win32/License.txt`, `win32com/License.txt`, `win32comext/License.txt`, `pythonwin/License.txt`, `pythonwin/pywin/idle/LICENSE.txt`, `pythonwin/Scintilla-License.txt`, `pythonwin/Scintilla/License.txt`, and `com/win32comext/mapi/src/MAPIStubLibrary/LICENSE`; all are retained in the bundled runtime |

`six` is the required transitive dependency declared by pystray. The
platform-specific pystray extras are not bundled. No other third-party
Python distribution is present in the final allowlisted site-packages.

## Native and standard-runtime components

| Component | Exact version | Bundled path | License identifier | Local license evidence / obligation |
| --- | --- | --- | --- | --- |
| OpenSSL | 3.5.5 | `runtime_env/python/DLLs/libcrypto-3-x64.dll`, `libssl-3-x64.dll` | Apache-2.0 | Version confirmed by the bundled runtime. The full Apache-2.0 text is retained in the installer payload. |
| libffi | 3.4.4 provenance pin; ABI 8 | `runtime_env/python/DLLs/libffi-8.dll`, used by `_ctypes.pyd` | MIT | DLL version resource is blank. The bundled runtime exposes ABI 8 and retains the matching MIT notice in the installer payload. |
| SQLite | 3.50.4 | `runtime_env/python/DLLs/sqlite3.dll`, `_sqlite3.pyd` | Public domain / SQLite blessing | Version confirmed by the bundled runtime. The public-domain notice is retained in the installer payload. |
| Tcl | 8.6.12 | `runtime_env/python/DLLs/tcl86t.dll`, `runtime_env/python/tcl/tcl8.6` | Tcl license, BSD-like permissive | `runtime_env/python/tcl/tk8.6/license.terms` and the Tcl/Tk terms in `runtime_env/python/LICENSE.txt`; retain notices verbatim. |
| Tk | 8.6.12 | `runtime_env/python/DLLs/tk86t.dll`, `runtime_env/python/tcl/tk8.6` | Tk license, BSD-like permissive | `runtime_env/python/tcl/tk8.6/license.terms` and the Tcl/Tk terms in `runtime_env/python/LICENSE.txt`; retain notices verbatim. |
| Tix | 8.4.3 | `runtime_env/python/tcl/tix8.4.3` | Tix/Tcl license, BSD-like permissive | Tix copyright and terms are included in `runtime_env/python/LICENSE.txt`; retain notices verbatim. |
| bzip2/libbzip2 | 1.0.8 | `runtime_env/python/DLLs/_bz2.pyd` | bzip2 license, BSD-like permissive | Full bzip2 text and copyright are included in `runtime_env/python/LICENSE.txt`; retain notice, conditions, and disclaimer. |
| XZ/liblzma | 5.2.5 provenance pin; binary version not exposed | `runtime_env/python/DLLs/_lzma.pyd` | Public domain (XZ Utils liblzma) | The bundled `_lzma.pyd` has no independent version resource. The matching notice is retained in the installer payload. |
| Expat | 2.7.4 | `runtime_env/python/DLLs/pyexpat.pyd` | MIT | Version confirmed by the bundled runtime. The full official notice is retained in the installer payload. |
| Scintilla | 4.4.6 | `runtime_env/python/Lib/site-packages/pythonwin/scintilla.dll` | Scintilla license, MIT-style permissive | Full text in `runtime_env/python/Lib/site-packages/pythonwin/Scintilla-License.txt`; copyright Neil Hodgson; retain notice and permission terms. |
| Microsoft Visual C++ runtime | version is part of the Python Windows build | `runtime_env/python/vcruntime140.dll`, `vcruntime140_1.dll` | Microsoft redistributable terms | Redistribution conditions are included in `runtime_env/python/LICENSE.txt`; do not alter Microsoft notices or use Microsoft trademarks to imply endorsement. |

The final payload also retains `runtime_env/python/LICENSE.txt`, the package
`.dist-info` license files, and the component-specific notices listed above.
The libffi and XZ versions are provenance pins from the official CPython
Windows runtime build because the bundled DLL/PYD resources do not expose
their own patch versions.

## Source offers and distribution obligations

The pystray 0.19.5 source offer is documented through its upstream package
source reference. The public distribution contains no LocalNetHealth source
tree. This notice and all referenced license texts must remain with the
installer distribution. No credentials, private contacts, or internal build
paths are included in this document.

## License retrieval provenance

The following notices originate from the official upstream sources and are
copied verbatim unless marked as the SQLite public-domain notice.

| Local file | Official source |
| --- | --- |
| `licenses/OPENSSL-3.5.5-LICENSE.txt` | `https://raw.githubusercontent.com/openssl/openssl/openssl-3.5.5/LICENSE.txt` |
| `licenses/LIBFFI-LICENSE-v3.4.4.txt` | `https://raw.githubusercontent.com/libffi/libffi/v3.4.4/LICENSE` |
| `licenses/XZ-5.2.5-COPYING.txt` | `https://raw.githubusercontent.com/tukaani-project/xz/v5.2.5/COPYING` |
| `licenses/EXPAT-2.7.4-COPYING.txt` | `https://raw.githubusercontent.com/libexpat/libexpat/R_2_7_4/COPYING` |
| `licenses/SQLITE-3.50.4-PUBLIC-DOMAIN.txt` | `https://www.sqlite.org/copyright.html` |

The version pins above are cross-referenced against the official CPython
3.12.13 Windows external-build manifest. The SQLite notice is a short
derived public-domain summary of the official SQLite copyright page.
