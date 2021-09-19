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

RUN git clone https://github.com/libp2p/rust-libp2p.git

WORKDIR /usr/src/myapp/rust-libp2p

RUN cargo build --release

