FROM selchenkov/rust-build:1.0.1

RUN git clone https://github.com/AleoHQ/snarkOS
WORKDIR /snarkOS
RUN source ~/.cargo/env && cargo build --release
