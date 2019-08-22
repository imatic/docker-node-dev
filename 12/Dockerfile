FROM node:12

RUN apt-get update && \
    apt-get install --yes jq equivs iceweasel xvfb postgresql-client-9.6 gnustep-make cgroup-tools awesome wmctrl ffmpeg openjdk-8-jdk pulseaudio && \
    sed -i 's/module-native-protocol-unix/\0 auth-anonymous=true/' /etc/pulse/system.pa && \
    # Update Firefox
    wget -O /opt/FirefoxSetup.tar.bz2 "https://download.mozilla.org/?product=firefox-latest&os=linux64&lang=en-US" && \
    mkdir /opt/firefox && \
    tar xjf /opt/FirefoxSetup.tar.bz2 -C /opt/firefox/ && \
    mv /usr/lib/firefox-esr/firefox-esr /usr/lib/firefox-esr/firefox-esr_orig && \
    ln -s /opt/firefox/firefox/firefox /usr/lib/firefox-esr/firefox-esr && \
    rm /opt/FirefoxSetup.tar.bz2 && \
    # Install geckodriver
    tag_name=$(curl --silent --show-error https://api.github.com/repos/mozilla/geckodriver/releases/latest | jq --raw-output '.tag_name') && \
    mkdir /opt/geckodriver && \
    curl --location --output /opt/geckodriver/geckodriver.tar.gz "https://github.com/mozilla/geckodriver/releases/download/${tag_name}/geckodriver-${tag_name}-linux64.tar.gz" && \
    tar -xvzf /opt/geckodriver/geckodriver.tar.gz -C /opt/geckodriver/ && \
    mv /opt/geckodriver/geckodriver /usr/local/bin && \
    rm -rf /opt/geckodriver && \
    # docker-tools
    equivs-control docker-ce.control && \
    sed -i 's/<package name; defaults to equivs-dummy>/docker-ce/g' docker-ce.control && \
    equivs-build docker-ce.control && \
    dpkg -i docker-ce_1.0_all.deb && \
    rm -rf ./docker-ce* && \
    curl --output docker-tools-latest.deb --location 'https://github.com/imatic/docker-tools/releases/download/1.1.2-1/docker-tools-1.1.2-1.deb' && \
    dpkg --install ./docker-tools-latest.deb || apt-get --fix-broken install --yes && dpkg --install ./docker-tools-latest.deb && \
    rm -rf ./docker-tools-latest.deb && \
    # cleanup
    rm -rf /var/lib/apt/lists/*
