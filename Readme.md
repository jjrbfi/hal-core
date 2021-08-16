In topdir:

    sudo apt-get install git

Linuxcnc old libs from buster repository:

    wget https://github.com/grotius-cnc/Linux-Pro/releases/download/1.0.0/libreadline5_5.2+dfsg-3+b13_amd64.deb
    wget https://github.com/grotius-cnc/Linux-Pro/releases/download/1.0.0/libreadline-gplv2-dev_5.2+dfsg-3+b13_amd64.deb
    dpkg -i libreadline5_5.2+dfsg-3+b13_amd64.deb
    dpkg -i libreadline-gplv2-dev_5.2+dfsg-3+b13_amd64.deb

Update sources to get dependencies:

    cat <<EOF > /etc/apt/sources.list
    deb http://ftp.de.debian.org/debian bullseye main contrib non-free
    deb-src http://ftp.de.debian.org/debian bullseye main contrib non-free
    deb http://security.debian.org/debian-security/ bullseye-security main
    deb-src http://security.debian.org/debian-security/ bullseye-security main
    EOF
    apt-get update

Install dependencies from bullseye and sid repository, not all of this is needed anymore, we can filter out dep's in future.

    sudo apt-get -y install debhelper libudev-dev tcl8.6-dev tk8.6-dev libtk-img bwidget tclx8.4 asciidoc \
    dblatex docbook-xsl dvipng graphviz groff source-highlight w3c-linkchecker xsltproc \
    texlive-extra-utils texlive-font-utils texlive-fonts-recommended texlive-lang-cyrillic texlive-lang-french \
    texlive-lang-german texlive-lang-polish texlive-lang-spanish texlive-latex-recommended \
    libxmu-dev libglu1-mesa-dev libgl1-mesa-dev libgtk2.0-dev libboost-python-dev \
    netcat libmodbus-dev libusb-1.0-0-dev yapps2 \
    gobject-introspection python3-gi python3-cairo-dev python3-gi-cairo python3-webview python3-pyqt5.qtsvg python3-opencv espeak \
    gstreamer1.0-python3-plugin-loader python3-intelhex libncurses-dev libtinfo-dev python3-tk \
    python3-xlib pyqt5-dev-tools qttools5-dev-tools intltool \

Install hal-core:

    $ cd src
    $ ./configure 
    $ make -j2
    $ sudo make setuid

Start app, in topdir:

    $ cd scripts && . ./rip-environment && cd ..

Load halcomponent:

    $ cd bin 
    $ halcmd loadrt yourcomponent 

Clean hal:

    $ cd bin && halrun -U 

If any problems occur try:

    $ sudo chown user -R rtapi_app
    $ sudo chown user -R linuxcnc_module_helper
    $ sudo chmod 777 rtapi_app
    $ sudo chmod 777 linuxcnc_module_helper
