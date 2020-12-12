FROM solnic/ruby:latest

ARG DEBIAN_FRONTEND=noninteractive

USER root

# install required devel packages
RUN apt-get update && \
  apt-get install -y --no-install-recommends pkg-config cmake && \
  apt-get clean

WORKDIR /pronto

COPY Gemfile* ./

RUN bundle install && \
  bundle binstubs --path /usr/local/bin --all
