FROM alpine:3.17
LABEL Author: @VITIMan https://github.com/VITIMan 

ENV MPD_VERSION 0.23.10-r3
ENV MPC_VERSION 0.34-r0

# https://docs.docker.com/engine/reference/builder/#arg
ARG user=mpd
ARG group=audio

RUN apk -q update \
    && apk -q --no-progress add mpd="$MPD_VERSION" \
    && apk -q --no-progress add mpc="$MPC_VERSION" \
    && rm -rf /var/cache/apk/*

RUN mkdir -p /var/lib/mpd/music \
    && mkdir -p /var/lib/mpd/playlists \
    && mkdir -p /var/lib/mpd/database \
    && mkdir -p /var/log/mpd/mpd.log \
    && chown -R ${user}:${group} /var/lib/mpd \
    && chown -R ${user}:${group} /var/log/mpd/mpd.log

# Declare a music , playlists and database volume (state, tag_cache and sticker.sql)
VOLUME ["/var/lib/mpd/music", "/var/lib/mpd/playlists", "/var/lib/mpd/database"]
COPY mpd.conf /etc/mpd.conf

# Entry point for mpc update and stuff
EXPOSE 6600

CMD ["mpd", "--stdout", "--no-daemon"]
