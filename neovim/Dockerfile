FROM solnic/ruby:latest

USER root

RUN apt-get install -y software-properties-common && \
    add-apt-repository ppa:neovim-ppa/unstable && \
    apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y neovim && \
    apt-get clean
