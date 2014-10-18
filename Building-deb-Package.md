Build package from source:

    sudo apt-get install build-essential automake libtool gawk debhelper
    git submodule update --init
    ./autogen.sh
    dpkg-buildpackage
    sudo dpkg -i ../shadowvpn_xxx.deb
