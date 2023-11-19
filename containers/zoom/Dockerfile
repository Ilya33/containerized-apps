ARG FROM=debian:11-slim
ARG WORKDIR=/var/workdir/containerized-apps



FROM $FROM

ARG WORKDIR

WORKDIR $WORKDIR

RUN apt-get update && \
    DEBIAN_FRODEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends --no-install-suggests \
        ca-certificates curl jq && \
    curl -fL "https://zoom.us/client/$(curl -sSL https://zoom.us/rest/download?os=linux | jq -r .result.downloadVO.zoom.version)/zoom_amd64.deb" \
        -o zoom.deb



FROM $FROM

ARG WORKDIR

RUN apt-get update && \
    DEBIAN_FRODEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends --no-install-suggests \
        # zoom.deb dependencies
        desktop-file-utils ibus libdbus-1-3 libdrm2 libfontconfig1 libgbm1 libglib2.0-0 libpulse0 libsm6 libsqlite3-0 \
        libxcb-cursor0 libxcb-icccm4 libxcb-image0 libxcb-keysyms1 libxcb-randr0 libxcb-shape0 libxcb-shm0 \
        libxcb-xfixes0 libxcb-xinerama0 libxcb-xtest0 libxcomposite1 libxi6 libxkbcommon-x11-0 libxrender1 libxslt1.1 \
        libxtst6 \
        # shared libraries
        libasound2 libgl1 libnss3

COPY --from=0 "$WORKDIR/zoom.deb" /tmp/

RUN cd /tmp/ && \
    dpkg -i zoom.deb && \
    apt-get clean && \
    rm /tmp/zoom.deb

ENTRYPOINT ["zoom", "--no-sandbox"]
