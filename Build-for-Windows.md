To run ShadowVPN, You need to install the TUN/TAP driver first:

* [For 32-bit Windows]
* [For 64-bit Windows]

It's recommended to build ShadowVPN on Debian, since it's simple.

### Build on Debian

Download a [release] and build.

    apt-get install build-essential mingw-w64
    ./configure --host=i686-w64-mingw32 --enable-static
    make

You'll find `shadowvpn.exe` in `src/`.

### Build on Windows

Download a [release] and build.

Currently only MinGW compilers are supported. You can compile in Msys or
cross-compile in Cygwin with 32-bit or 64-bit MinGW toolchains.

For example, if using 64-bit Cygwin, install `libtool`, `autoconf`
and `mingw64-x86_64-gcc-g++` by Cygwin installer. Then Download a [release]
and build. Build from Cygwin terminal by the following commands:

    ./configure --host=x86_64-w64-mingw32 --enable-static
    make && make install DESTDIR="$HOME/shadowvpn-build"

Executables will be generated in `$HOME/shadowvpn-build`.


[For 32-bit Windows]:   http://build.openvpn.net/downloads/releases/tap-windows-9.9.2_3.exe
[For 64-bit Windows]:   http://build.openvpn.net/downloads/releases/tap-windows-9.21.0.exe
[release]:              https://github.com/clowwindy/ShadowVPN/releases