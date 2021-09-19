FROM rust:alpine3.14 AS builder

RUN \
  apk add --no-cache --upgrade \
    git \
    musl-dev

RUN \
    apk add --no-cache openssl-dev

RUN rustup toolchain install nightly

RUN rustup default nightly

WORKDIR /usr/src/myapp

RUN git clone --branch testnet https://gitlab.com/massalabs/massa.git

WORKDIR /usr/src/myapp/massa/massa-node

RUN cargo build --release

WORKDIR /usr/src/myapp/massa/massa-client

RUN cargo build --release

RUN ls -la  /usr/src/myapp/massa/target/release/massa-node
RUN ls -la  /usr/src/myapp/massa/target/release/massa-client

FROM ghcr.io/linuxserver/openssh-server:latest

RUN \
  apk add --no-cache --upgrade \
    git \
    musl

RUN \
    apk add --no-cache openssl

RUN mkdir -p /app/massa/massa-node/base_config
RUN mkdir -p /app/massa/massa-client/base_config
RUN mkdir -p /app/massa/massa-node/config
RUN mkdir -p /app/massa/massa-client/config
RUN mkdir -p /app/massa/massa-node/storage

COPY --from=builder /usr/src/myapp/massa/target/release/massa-node /app/massa/massa-node
COPY --from=builder /usr/src/myapp/massa/target/release/massa-client /app/massa/massa-client

COPY --from=builder /usr/src/myapp/massa/massa-node/base_config /app/massa/massa-node/base_config
COPY --from=builder /usr/src/myapp/massa/massa-node/config /app/massa/massa-node/config
COPY --from=builder /usr/src/myapp/massa/massa-node/storage /app/massa/massa-node/storage

COPY --from=builder /usr/src/myapp/massa/massa-client/base_config /app/massa/massa-client/base_config
COPY --from=builder /usr/src/myapp/massa/massa-client/config /app/massa/massa-client/config

RUN chown -R 1000:1000 /app

