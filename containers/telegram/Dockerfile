ARG FROM=debian:11-slim
ARG WORKDIR=/var/build/app_in_container



FROM $FROM

ARG WORKDIR

WORKDIR $WORKDIR

RUN apt-get update && \
    DEBIAN_FRODEBIAN_FRONTEND=noninteractive apt-get install -y wget xz-utils && \
    wget --content-disposition https://telegram.org/dl/desktop/linux
RUN ls
RUN tar xf "$(ls)"



FROM $FROM

ARG WORKDIR

COPY --from=0 "$WORKDIR/Telegram" /opt/Telegram

RUN apt-get update && \
    DEBIAN_FRODEBIAN_FRONTEND=noninteractive apt-get install -y libfontconfig1 libglib2.0-0 libgl1 libgtk-3-0 \
    libx11-xcb1 libx11-6

ENTRYPOINT ["/opt/Telegram/Telegram"]
