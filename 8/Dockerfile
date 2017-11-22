FROM node:8

RUN echo "deb http://apt.postgresql.org/pub/repos/apt/ jessie-pgdg main" > /etc/apt/sources.list.d/pgdg.list && \
    wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add - && \
    echo "deb http://http.debian.net/debian jessie-backports main" >>  /etc/apt/sources.list && \
    apt-get update && \
    apt-get install --yes iceweasel xvfb postgresql-client-9.6 && \
    apt-get install --yes -t jessie-backports openjdk-8-jdk && \

    # Update Firefox
    wget -O /opt/FirefoxSetup.tar.bz2 "https://download.mozilla.org/?product=firefox-latest&os=linux64&lang=en-US" && \
    mkdir /opt/firefox && \
    tar xjf /opt/FirefoxSetup.tar.bz2 -C /opt/firefox/ && \
    mv /usr/lib/firefox-esr/firefox-esr /usr/lib/firefox-esr/firefox-esr_orig && \
    ln -s /opt/firefox/firefox/firefox /usr/lib/firefox-esr/firefox-esr

