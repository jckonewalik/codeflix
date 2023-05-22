FROM golang:1.19-alpine
ENV PATH="$PATH:/bin/bash" \
    BENTO4_BIN="/opt/bento4/bin" \
    PATH="$PATH:/opt/bento4/bin"

RUN apk add --update ffmpeg bash curl make cmake

WORKDIR /tmp/bento4
ENV BENTO4_BASE_URL="http://zebulon.bok.net/Bento4/source/" \
    BENTO4_VERSION="1-6-0-639" \
    BENTO4_CHECKSUM="d3351ffb425aadc698227ba84f5ec3401cad795a" \
    BENTO4_TARGET="" \
    BENTO4_PATH="/opt/bento4" \
    BENTO4_TYPE="SRC"

RUN apk add --update --upgrade curl python3 unzip bash gcc g++ git && \
    curl -O -s ${BENTO4_BASE_URL}/Bento4-${BENTO4_TYPE}-${BENTO4_VERSION}${BENTO4_TARGET}.zip && \
    sha1sum -b Bento4-${BENTO4_TYPE}-${BENTO4_VERSION}${BENTO4_TARGET}.zip | grep -o "^$BENTO4_CHECKSUM " && \
    unzip Bento4-${BENTO4_TYPE}-${BENTO4_VERSION}${BENTO4_TARGET}.zip -d . && \
    rm -rf Bento4-${BENTO4_TYPE}-${BENTO4_VERSION}${BENTO4_TARGET}.zip && \
    apk del unzip && \
    mkdir cmakebuild && cd cmakebuild && \
    cmake -DCMAKE_BUILD_TYPE=Release .. && \
    make AP4_BUILD_CONFIG=Release && \
    mkdir -p ${BENTO4_PATH}/bin && mv ./* ${BENTO4_PATH}/bin

WORKDIR /go/src

RUN rm -rf /tmp/bento4

ENTRYPOINT ["tail", "-f", "/dev/null"]