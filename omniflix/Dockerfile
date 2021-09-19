FROM golang:1.17-alpine3.14 AS builder

WORKDIR /go/src/app

RUN \
  apk add --no-cache --upgrade git build-base make jq

RUN git clone https://github.com/Omniflix/omniflixhub.git

WORKDIR /go/src/app/omniflixhub

RUN git fetch --all
RUN git checkout v0.2.1
RUN make install

RUN omniflixhubd version --long

FROM ghcr.io/linuxserver/openssh-server:latest

RUN mkdir -p /app/omniflixhubd

COPY --from=builder /go/bin/omniflixhubd /app/omniflixhubd

RUN chown -R 1000:1000 /app
