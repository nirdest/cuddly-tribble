FROM debian:bullseye-slim

ARG FREESWITCH_VERSION=1.10.7
ARG TOKEN=$API_KEY_FROM_SIGNALWIRE
ARG LOGIN=signalwire

RUN apt-get update -qq \
    && apt-get -y install --quiet --no-install-recommends apt-transport-https ca-certificates curl gnupg2 lsb-release pkg-config wget \
    && wget --user=$LOGIN --password=$TOKEN -O /usr/share/keyrings/signalwire-freeswitch-repo.gpg https://freeswitch.signalwire.com/repo/deb/debian-release/signalwire-freeswitch-repo.gpg \
    && echo "machine freeswitch.signalwire.com login $LOGIN password $TOKEN" > /etc/apt/auth.conf \
    && chmod 600 /etc/apt/auth.conf \
    && echo "deb [signed-by=/usr/share/keyrings/signalwire-freeswitch-repo.gpg] https://freeswitch.signalwire.com/repo/deb/debian-release/ `lsb_release -sc` main" > /etc/apt/sources.list.d/freeswitch.list \
    && echo "deb-src [signed-by=/usr/share/keyrings/signalwire-freeswitch-repo.gpg] https://freeswitch.signalwire.com/repo/deb/debian-release/ `lsb_release -sc` main" >> /etc/apt/sources.list.d/freeswitch.list \
    && apt-get update \
    && export FREESWITCH_RELEASE_VERSION=`apt-cache policy freeswitch | grep -E "^\s+$FREESWITCH_VERSION" | awk '{print $1}'` \
    && apt-get -y install --quiet --no-install-recommends \
        libfreeswitch1=${FREESWITCH_RELEASE_VERSION} \
        freeswitch=${FREESWITCH_RELEASE_VERSION} \
        freeswitch-mod-console=${FREESWITCH_RELEASE_VERSION} \
        freeswitch-mod-logfile=${FREESWITCH_RELEASE_VERSION} \
        freeswitch-mod-xml-curl=${FREESWITCH_RELEASE_VERSION} \
        freeswitch-mod-sofia=${FREESWITCH_RELEASE_VERSION} \
        freeswitch-mod-loopback=${FREESWITCH_RELEASE_VERSION} \
        freeswitch-mod-rtc=${FREESWITCH_RELEASE_VERSION} \
        freeswitch-mod-event-socket=${FREESWITCH_RELEASE_VERSION} \
        freeswitch-mod-commands=${FREESWITCH_RELEASE_VERSION} \
        freeswitch-mod-db=${FREESWITCH_RELEASE_VERSION} \
        freeswitch-mod-dptools=${FREESWITCH_RELEASE_VERSION} \
        freeswitch-mod-expr=${FREESWITCH_RELEASE_VERSION} \
        freeswitch-mod-hash=${FREESWITCH_RELEASE_VERSION} \
        freeswitch-mod-esf=${FREESWITCH_RELEASE_VERSION} \
        freeswitch-mod-dialplan-xml=${FREESWITCH_RELEASE_VERSION} \
        freeswitch-mod-dialplan-asterisk=${FREESWITCH_RELEASE_VERSION} \
        freeswitch-mod-spandsp=${FREESWITCH_RELEASE_VERSION} \
        freeswitch-mod-g723-1=${FREESWITCH_RELEASE_VERSION} \
        freeswitch-mod-g729=${FREESWITCH_RELEASE_VERSION} \
        freeswitch-mod-amr=${FREESWITCH_RELEASE_VERSION} \
        freeswitch-mod-b64=${FREESWITCH_RELEASE_VERSION} \
        freeswitch-mod-opus=${FREESWITCH_RELEASE_VERSION} \
        freeswitch-mod-sndfile=${FREESWITCH_RELEASE_VERSION} \
        freeswitch-mod-native-file=${FREESWITCH_RELEASE_VERSION} \
        freeswitch-mod-local-stream=${FREESWITCH_RELEASE_VERSION} \
        freeswitch-mod-tone-stream=${FREESWITCH_RELEASE_VERSION} \
    && apt-get purge -qq -y --auto-remove git \
    && rm -rf /var/lib/apt/lists/*

USER 999:999
ENTRYPOINT ["/usr/bin/freeswitch"]
CMD ["-c", "-u", "freeswitch", "-g", "freeswitch", "-nonat"]

