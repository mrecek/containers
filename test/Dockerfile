FROM ubuntu:jammy-20220531
LABEL org.opencontainers.image.title="CI-CD general image"
LABEL org.opencontainers.image.authors="Mark Recek (mark@recek.com)"
# To prevent interactive prompts from apt commands
ENV DEBIAN_FRONTEND=noninteractive
# Install dependancies
RUN apt update && apt install -y python3 python3-pip python-is-python3 gnupg2 curl openssh-server software-properties-common
# Install Ansible
RUN apt install -y ansible
# Install Terraform
RUN curl https://apt.releases.hashicorp.com/gpg | gpg --dearmor > hashicorp.gpg \
    && install -o root -g root -m 644 hashicorp.gpg /etc/apt/trusted.gpg.d/ \
    && apt-add-repository "deb [arch=$(dpkg --print-architecture)] https://apt.releases.hashicorp.com focal main" \
    && apt update && apt install -y terraform
# Cleanup cached apt lists
RUN rm -rf /var/lib/apt/lists/*
RUN service ssh start
CMD ["/bin/bash"]