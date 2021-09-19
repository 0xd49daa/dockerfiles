FROM archlinux:latest

RUN pacman -Sy --needed --noconfirm \
  sudo which vim tar grep sed awk wget openssh git

RUN pacman -Sc --noconfirm

ENV EDITOR='vim'

RUN sed -ie 's/^#\(en_US\.UTF-8 UTF-8\)/\1/' /etc/locale.gen \
  && locale-gen

RUN useradd -mU -s /bin/bash akash && echo 'akash:akash' | chpasswd

RUN echo "akash ALL=(ALL:ALL) ALL" | (EDITOR="tee -a" visudo)

RUN echo "AllowUsers akash" >> /etc/ssh/sshd_config
RUN echo "PasswordAuthentication no" >> /etc/ssh/sshd_config

RUN ssh-keygen -A

USER akash

RUN mkdir -p /home/akash/.ssh

RUN touch ~/.ssh/authorized_keys

RUN echo "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC728CxtrIQxTX1QQLRDWWAtBi7WzpueZJ8zJPqYjczGcmw0pI6s2yl7/Ntx9zPP9J+nzOMw1nGozhoCPp4vO9DsaezDCsQcEfzJ6TpJRYlR+1WgLQr1qbKh2K3uZReogEGjflpGDiwW44SD4pNJwy+t06+k4h8LkUme2Z0F7wdK9crvEfZyi3AjTPMfpzBytxBWIYwfv3R+59E5eYFrPE2UKJXZna0ODYxsi5a5NfvCec0vtSyPI0mftGDeJJMODca51azeIEeLPVKvpcBCpw2m1638YFgedZtKHjCDFvTlNyc0fNIpugscqYC7Fn/OFHKy+npsD/SHB/93Sd1zwPJaj89ddiEfveuwSQMi6SftkztD8unGReyzMoIt0QVrA2T+4UfdVTeXPPn0WUkEWJx5DIcZYrimT3wNEI2G4m8UluG4VN/loD6HvTD9B7B1ry3awQSoWJsJnvNz4k/acfRdhWlK9U6TscxELdB3W3t0bnSCF4WN8wMDAwUP3o6IWM= ledger@work" >> ~/.ssh/authorized_keys

RUN chmod 700 ~/.ssh
RUN chmod 600 ~/.ssh/authorized_keys

USER root

CMD /bin/sshd -D