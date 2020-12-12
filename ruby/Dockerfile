FROM ubuntu:latest

USER root

# install required devel packages
RUN apt-get update && \
    apt-get install -y --no-install-recommends apt-utils sudo wget build-essential ca-certificates && \
    apt-get clean

WORKDIR /tmp

RUN wget -O ruby-install-0.7.1.tar.gz https://github.com/postmodern/ruby-install/archive/v0.7.1.tar.gz && \
tar -xzvf ruby-install-0.7.1.tar.gz && \
cd ruby-install-0.7.1 && \
make install && \
rm -rf /tmp/ruby-install-0.7.1

RUN wget -O chruby-0.3.9.tar.gz https://github.com/postmodern/chruby/archive/v0.3.9.tar.gz && \
tar -xzvf chruby-0.3.9.tar.gz && \
cd chruby-0.3.9 && \
./scripts/setup.sh && \
rm -rf /tmp/chruby-0.3.9

SHELL [ "/bin/bash", "-l", "-c" ]

# install latest stable ruby
RUN ruby-install -c -j4 -c --latest ruby --system -- --disable-install-rdoc && \
    sudo apt-get clean && \
    echo "source /usr/local/share/chruby/chruby.sh" >> ~/.bash_profile && \
    echo "source /usr/local/share/chruby/auto.sh" >> ~/.bash_profile && \
    echo "ruby" >> ~/.ruby-version

# install latest bundler
RUN chruby 2.7; gem install bundler --no-document

RUN useradd -m -U -s /bin/bash -G root,sudo ruby && \
  echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

USER ruby

ENTRYPOINT [ "/bin/bash", "-l" ]
