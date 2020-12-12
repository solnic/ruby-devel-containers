FROM solnic/ruby:latest

ARG DEBIAN_FRONTEND=noninteractive

USER root

# install required devel packages
RUN apt-get update && \
    apt-get install -y --no-install-recommends pkg-config cmake && \
    apt-get clean

WORKDIR /tmp

COPY Gemfile* ./

RUN bundle install
