FROM selchenkov/rust-build:1.0.1 AS builder

RUN git clone https://github.com/AleoHQ/snarkOS
WORKDIR /snarkOS
RUN source ~/.cargo/env && cargo build --release

FROM selchenkov/base:1.0.1

COPY --from=builder /snarkOS/target/release/snarkos /app/snarkos

