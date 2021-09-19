FROM atlassian/ssh-ubuntu AS builder

RUN apt update
RUN apt install -y git clang curl libssl-dev llvm libudev-dev

RUN curl https://getsubstrate.io -sSf | bash -s -- --fast

RUN git clone https://github.com/porta-network/porta-node.git

RUN cd porta-node/ && bash -c 'source ~/.cargo/env && cargo build --release'

FROM atlassian/ssh-ubuntu

RUN apt update
RUN apt install -y git clang curl libssl-dev llvm libudev-dev openssh-server

COPY --from=builder /porta-node/chain-spec-padlock.json /app/
COPY --from=builder /porta-node/target/release/porta /app/

RUN chown -R 1000:1000 /app
