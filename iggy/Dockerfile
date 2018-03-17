# Use phusion/baseimage as base image
# Lock down to a specific version, see
# https://github.com/phusion/baseimage-docker/blob/master/Changelog.md
# for a list of version numbers
FROM phusion/baseimage:0.10.0
MAINTAINER Fernando Rivas <fenandos@hotmail.com>

# Use baseimage-docker's init system
CMD ["/sbin/my_init"]

# Set environment variables
ENV HOME /root

# Update base system
RUN apt-get update && apt-get -y upgrade \ 
      && apt-get install -y language-pack-en \
      && locale-gen en_US.UTF-8 \
      && dpkg-reconfigure locales

# Install basic packages
RUN apt-get install -y build-essential software-properties-common wget curl git man unzip nano tmux colord zsh emacs vim

# Install zsh
RUN git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh \
      && cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc \
      && chsh -s /bin/zsh

WORKDIR /root
CMD ["zsh"]

# Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
