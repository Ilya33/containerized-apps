ARG FROM=debian:11-slim
ARG WORKDIR=/var/workdir/containerized-apps



FROM $FROM

ARG WORKDIR

WORKDIR $WORKDIR

RUN apt-get update && \
    DEBIAN_FRODEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends --no-install-suggests \
        ca-certificates wget xz-utils && \
    wget --content-disposition https://telegram.org/dl/desktop/linux && \
    tar xf "$(ls)"



FROM $FROM

ARG WORKDIR

RUN apt-get update && \
    DEBIAN_FRODEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends --no-install-suggests \
        fonts-wqy-zenhei libfontconfig1 libglib2.0-0 libgl1 libgtk-3-0 libx11-xcb1 libx11-6 && \
    apt-get clean

COPY --from=0 "$WORKDIR/Telegram" /opt/Telegram

ENTRYPOINT ["/opt/Telegram/Telegram"]
