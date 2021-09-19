FROM rust:alpine3.14 AS builder

RUN \
  apk add \
    git \
    musl-dev \
    bash \
    llvm \
    clang \
    llvm-dev

RUN \
    apk add --no-cache openssl-dev protoc

WORKDIR /usr/src/myapp

RUN git clone https://github.com/dappforce/subsocial-node.git

WORKDIR /usr/src/myapp/subsocial-node

RUN ./scripts/init.sh

RUN RUST_BACKTRACE=1 cargo build --release

# FROM ghcr.io/linuxserver/openssh-server:latest

# RUN \
#   apk add --no-cache --upgrade \
#     git \
#     musl

# RUN \
#     apk add --no-cache openssl

# RUN mkdir -p /app/massa/massa-node/base_config
# RUN mkdir -p /app/massa/massa-client/base_config
# RUN mkdir -p /app/massa/massa-node/config
# RUN mkdir -p /app/massa/massa-client/config
# RUN mkdir -p /app/massa/massa-node/storage

# COPY --from=builder /usr/src/myapp/massa/target/release/massa-node /app/massa/massa-node
# COPY --from=builder /usr/src/myapp/massa/target/release/massa-client /app/massa/massa-client

# COPY --from=builder /usr/src/myapp/massa/massa-node/base_config /app/massa/massa-node/base_config
# COPY --from=builder /usr/src/myapp/massa/massa-node/config /app/massa/massa-node/config
# COPY --from=builder /usr/src/myapp/massa/massa-node/storage /app/massa/massa-node/storage

# COPY --from=builder /usr/src/myapp/massa/massa-client/base_config /app/massa/massa-client/base_config
# COPY --from=builder /usr/src/myapp/massa/massa-client/config /app/massa/massa-client/config

# RUN chown -R 1000:1000 /app

