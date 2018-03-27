FROM phusion/passenger-customizable:latest
MAINTAINER Fernando Rivas <fenandos@hotmail.com>

# Set correct environment variables.
ENV HOME /root

# Use baseimage-docker's init process.
CMD ["/sbin/my_init"]

# built-in packages
RUN apt-get update \
    && apt-get install -y --no-install-recommends --allow-unauthenticated \
        supervisor net-tools \
        lxde x11vnc xvfb \
        ttf-ubuntu-font-family \
        firefox \
        python-pip python-dev build-essential \
        libc6-dev libpango1.0-dev libx11-dev libgl1-mesa-dev \
        xorg-dev libgtk2.0-dev gtk2-engines-pixbuf libgtkglext1-dev rlwrap \
        mesa-utils libgl1-mesa-dri \
        gnome-themes-standard gtk2-engines-pixbuf gtk2-engines-murrine pinta arc-theme \
        dbus-x11 x11-utils

# Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# tini for subreap
ARG TINI_VERSION=v0.9.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /bin/tini
RUN chmod +x /bin/tini

ADD image/usr/lib/web/requirements.txt /tmp/
RUN pip install --upgrade pip
RUN pip install setuptools wheel && pip install -r /tmp/requirements.txt
ADD image /

EXPOSE 80
WORKDIR /root
ENV HOME=/home/ubuntu
ENTRYPOINT ["/startup.sh"]
