# Text workflow Docker based on TeX Live
FROM debian_devcontainer:bookworm AS build
LABEL author="Juan Pedro Perez"
LABEL author_email="jp.perez.alcantara@gmail.com"
LABEL maintainer="Juan Pedro Perez"
LABEL maintainer_email="jp.perez.alcantara@gmail.com"
LABEL description="Text workflow Docker based on TeX Live. To be used as a DevContainer."

WORKDIR /

USER root

# Package configuration
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get dist-upgrade -y && \
    apt-get update && \
    apt-get install -y \
      imagemagick \
      libncurses5 \
      python3 \
      python3-pip \
      git-flow \
      chromium \
      fonts-liberation \
      libappindicator3-1 \
      libasound2 \
      libatk-bridge2.0-0 \
      libatk1.0-0 \
      libcups2 \
      libdbus-1-3 \
      libgdk-pixbuf2.0-0 \
      libnspr4 \
      libnss3 \
      libx11-xcb1 \
      libxcomposite1 \
      libxdamage1 \
      libxrandr2 \
      xdg-utils


RUN ldconfig

RUN ln -s /usr/bin/python3 /usr/bin/python

RUN python3 -m pip install --upgrade --break-system-packages \
  mkdocs \
  mkdocs-material \
  mkdocs-bootswatch \
  watchdog \
  jinja2

# Add assets
COPY assets/pandoc*.deb /pandoc.deb

# Install pandoc
RUN dpkg -i /pandoc.deb && \
  rm /pandoc.deb

# Clean a little bit
RUN rm -rf /var/lib/apt/lists/* /var/cache/apt/* /var/log/dpkg.log /var/log/apt/* && \
    apt-get clean && \
    rm -rf /var/lib/dpkg/*-old

USER vscode