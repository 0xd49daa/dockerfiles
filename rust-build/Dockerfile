FROM archlinux:latest

RUN pacman -Sy git base-devel clang --noconfirm --needed

RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y
