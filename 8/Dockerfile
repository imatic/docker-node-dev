FROM node:8

RUN echo "deb http://apt.postgresql.org/pub/repos/apt/ jessie-pgdg main" > /etc/apt/sources.list.d/pgdg.list && \
    wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add - && \
    echo "deb http://http.debian.net/debian jessie-backports main" >>  /etc/apt/sources.list && \
    apt-get update && \
    apt-get install --yes iceweasel xvfb postgresql-client-9.6 gnustep-make cgroup-tools awesome wmctrl ffmpeg && \
    apt-get install --yes -t jessie-backports openjdk-8-jdk pulseaudio && \
    sed -i 's/module-native-protocol-unix/\0 auth-anonymous=true/' /etc/pulse/system.pa && \

    # Update Firefox
    wget -O /opt/FirefoxSetup.tar.bz2 "https://download.mozilla.org/?product=firefox-latest&os=linux64&lang=en-US" && \
    mkdir /opt/firefox && \
    tar xjf /opt/FirefoxSetup.tar.bz2 -C /opt/firefox/ && \
    mv /usr/lib/firefox-esr/firefox-esr /usr/lib/firefox-esr/firefox-esr_orig && \
    ln -s /opt/firefox/firefox/firefox /usr/lib/firefox-esr/firefox-esr && \

    # docker-tools
    curl --output docker-tools-latest.deb --location 'https://github.com/imatic/docker-tools/releases/download/1.1.2-1/docker-tools-1.1.2-1.deb' && \
    dpkg --install --ignore-depends docker-ce ./docker-tools-latest.deb || apt-get --fix-broken install --yes && dpkg --install --ignore-depends docker-ce ./docker-tools-latest.deb && \
    rm -rf ./docker-tools-latest.deb && \


    rm -rf /var/lib/apt/lists/*
