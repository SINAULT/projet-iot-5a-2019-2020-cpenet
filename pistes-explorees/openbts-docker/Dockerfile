FROM ubuntu:xenial

ENV APT="apt-get -y"

USER root
ENV DEBIAN_FRONTEND=noninteractive
RUN ${APT} update && ${APT} upgrade
RUN ${APT} install software-properties-common
RUN ${APT} update || true
RUN echo "resolvconf resolvconf/linkify-resolvconf boolean false" | debconf-set-selections
RUN ${APT} install locales python-software-properties build-essential git-core cmake g++ python-dev swig pkg-config libfftw3-dev libboost-all-dev libcppunit-dev libgsl-dev libusb-dev libsdl1.2-dev python-wxgtk3.0 python-numpy python-cheetah python-lxml doxygen libxi-dev python-sip libqt4-opengl-dev libfontconfig1-dev libxrender-dev zeroc-ice35 libzeroc-ice35-dev python-sphinx python-scipy libpulse-dev automake autoconf libtool libusb-1.0-0-dev fort77 libqt4-dev ccache python-opengl qt4-default qt4-dev-tools libqwt-dev libqwtplot3d-qt4-dev pyqt4-dev-tools python-qwt5-qt4 python-docutils gtk2-engines-pixbuf r-base-dev python-tk liborc-0.4-0 liborc-0.4-dev libasound2-dev python-gtk2 libzmq3-dev libcomedi-dev python-zmq psmisc erlang libreadline6-dev bind9 ntp ntpdate python-pip python-requests libgsl0-dev python-wxgtk3.0 debhelper sqlite3 libsqlite3-dev libortp-dev libosip2-dev libsqlite0-dev unixodbc unixodbc-dev libssl-dev libsrtp0 libsrtp0-dev libjansson-dev libxml2-dev libzmq5 libsqliteodbc wget sudo liblog4cpp5-dev libfftw3-3 libqwt5-qt4 libusb-1.0-0 python-cairo-dev python-mako python-qt4 git libortp9 libreadline-dev libncurses5 libncurses5-dev cdbs uuid-dev dpkg-dev resolvconf
RUN pip install --upgrade pip
RUN pip install mako
RUN adduser --disabled-password cxlbadm
RUN adduser cxlbadm sudo
RUN sed -i -e 's%cxlbadm:\*:%cxlbadm:$6$fEFUE2YaNmTEH51Z$1xRO8/ytEYIo10ajp4NZSsoxhCe1oPLIyjDjqSOujaPZXFQxSSxu8LDHNwbPiLSjc.8u0Y0wEqYkBEEc5/QN5/:%' /etc/shadow

RUN ${APT} install libuhd-dev libuhd003 uhd-host
RUN add-apt-repository ppa:ettusresearch/uhd
RUN ${APT} update || true

WORKDIR /home/cxlbadm
RUN git clone https://github.com/RangeNetworks/dev.git
WORKDIR /home/cxlbadm/dev/
RUN ./clone.sh
RUN ./switchto.sh master
RUN ${APT} install asterisk

RUN mkdir BUILDS
WORKDIR /home/cxlbadm/dev/BUILDS/
COPY ./liba53_0.1_arm64.deb liba53_0.1_arm64.deb
COPY ./sipauthserve_5.0_arm64.deb sipauthserve_5.0_arm64.deb
COPY ./smqueue_5.0_arm64.deb smqueue_5.0_arm64.deb
RUN dpkg -i *.deb

WORKDIR /home/cxlbadm/dev/asterisk-config/
RUN sudo cp *.conf /etc/asterisk/
RUN sudo cp *.ini /etc/
WORKDIR /home/cxlbadm/dev/asterisk-config/en/
RUN sudo cp *.gsm /var/lib/asterisk/sounds/custom/

WORKDIR /home/cxlbadm
RUN sudo git clone --recursive https://github.com/nadiia-kotelnikova/openbts_systemd_scripts.git
RUN cp -r /home/cxlbadm/openbts_systemd_scripts/systemd/. /etc/systemd/system/
RUN sed -i "s/^Description=sipauthserve$/Description=sipauthserve\nRequires=asterisk.service\nAfter=asterisk.service/" /etc/systemd/system/sipauthserve.service
RUN sed -i "s/^Description=smqueue$/Description=smqueue\nRequires=sipauthserve.service\nAfter=sipauthserve.service/" /etc/systemd/system/smqueue.service
RUN sed -i "s/^Description=OpenBTS$/Description=OpenBTS\nRequires=smqueue.service\nAfter=smqueue.service/" /etc/systemd/system/openbts.service

RUN systemctl enable openbts

WORKDIR /OpenBTS
CMD [ "/sbin/init" ]

RUN ${APT} install openssh-server
RUN sed -i 's/^Port 22$/Port 39775/' /etc/ssh/sshd_config
RUN sed -i 's/^PermitEmptyPasswords no$/PermitEmptyPasswords yes/' /etc/ssh/sshd_config



