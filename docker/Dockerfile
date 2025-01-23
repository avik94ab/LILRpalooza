FROM ubuntu:latest
RUN apt-get update && apt-get install -y locales && rm -rf /var/lib/apt/lists/* \
    && localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8
RUN apt-get update
RUN apt-get install -y build-essential
RUN apt-get install -y git zlib1g-dev curl
RUN mkdir -p /opt/
RUN cd /opt/ && git clone https://github.com/lh3/miniprot.git
RUN cd /opt/miniprot && make
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y
RUN apt-get install -y openssl pkg-config libssl-dev
RUN touch /trigger
RUN cd /opt/ && git clone https://github.com/cschin/LILRpalooza.git
RUN cd /opt/LILRpalooza/server && . $HOME/.cargo/env && cargo build --release
ENV LANG en_US.utf8
RUN mkdir -p /opt/bin/ && cp /opt/miniprot/miniprot /opt/bin/
RUN cp -a /opt/LILRpalooza/server/ref_data/ /opt/ref_data/
CMD /opt/LILRpalooza/server/target/release/server
