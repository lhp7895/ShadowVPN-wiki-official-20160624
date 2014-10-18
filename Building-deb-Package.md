Build package from source:

    sudo apt-get install build-essential automake libtool gawk debhelper
    git submodule update --init
    ./autogen.sh
    dpkg-buildpackage
    cd ..
    sudo dpkg -i shadowvpn*.deb
