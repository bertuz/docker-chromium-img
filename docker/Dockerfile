FROM debian:unstable-20211011-slim

# install required packages and utilities
RUN apt-get update && apt-get install -y --no-install-recommends \
    ca-certificates \
    apt-utils \
    locales \
    curl \
    git \
    unzip \
    procps

# chrome dependencies for puppeteer installed chrome
# see https://github.com/puppeteer/puppeteer/blob/main/docs/troubleshooting.md#chrome-headless-doesnt-launch-on-unix
# and https://github.com/puppeteer/puppeteer/issues/7822
RUN apt-get install -y --no-install-recommends \
    fonts-liberation \
    libayatana-appindicator3-1 \
    libasound2 \
    libatk-bridge2.0-0 \
    libatk1.0-0 \
    libc6 \
    libcairo2 \
    libcups2 \
    libdbus-1-3 \
    libexpat1 \
    libfontconfig1 \
    libgbm1 \
    libgcc1 \
    libglib2.0-0 \
    libgtk-3-0 \
    libnspr4 \
    libnss3 \
    libpango-1.0-0 \
    libpangocairo-1.0-0 \
    libstdc++6 \
    libx11-6 \
    libx11-xcb1 \
    libxcb1 \
    libxcomposite1 \
    libxcursor1 \
    libxdamage1 \
    libxext6 \
    libxfixes3 \
    libxi6 \
    libxrandr2 \
    libxrender1 \
    libxss1 \
    libxtst6 \
    lsb-release \
    wget \
    xdg-utils

# setup locale
RUN sed -i -e 's/# es_ES.UTF-8 UTF-8/es_ES.UTF-8 UTF-8/' /etc/locale.gen && \
    dpkg-reconfigure --frontend=noninteractive locales

# install chromium
# IMPORTANT the chromium version must be the same as the one used by puppeteer in acceptance-testing package
RUN apt-get update && apt-get install -y --no-install-recommends \
    chromium-bsu chromium-shell chromium-sandbox chromium-common

# install nodejs and related stuff
RUN curl -sL https://deb.nodesource.com/setup_16.x | bash -
RUN apt-get update && apt-get install -y --no-install-recommends \
    nodejs \
    gcc \
    g++ \
    make
RUN npm install -g yarn@^1.22.15

ENV TZ UTC
ENV LANGUAGE es_ES.UTF-8
ENV LANG es_ES.UTF-8
ENV LC_ALL es_ES.UTF-8

CMD ["/usr/bin/chromium", \
    "--lang=es_ES", \
    # flags from https://github.com/GoogleChrome/puppeteer/blob/master/lib/Launcher.js
    "--disable-background-networking", \
    "--disable-background-timer-throttling", \
    "--disable-breakpad", \
    "--disable-client-side-phishing-detection", \
    "--disable-default-apps", \
    "--disable-dev-shm-usage", \
    "--disable-extensions", \
    "--disable-features=site-per-process", \
    "--disable-hang-monitor", \
    "--disable-popup-blocking", \
    "--disable-prompt-on-repost", \
    "--disable-sync", \
    "--disable-translate", \
    "--metrics-recording-only", \
    "--no-first-run", \
    "--safebrowsing-disable-auto-update", \
    "--enable-automation", \
    "--password-store=basic", \
    "--use-mock-keychain", \
    "--headless", \
    "--hide-scrollbars", \
    # Disable sandbox mode
    "--no-sandbox", \
    # Avoids font rendering differences between headless/headfull
    "--font-render-hinting=none", \
    # Expose port 9222 for remote debugging
    "--remote-debugging-port=9222", \
    "--remote-debugging-address=0.0.0.0", \
    "--ignore-certificate-errors" \
    ]
