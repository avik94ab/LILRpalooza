FROM ubuntu:latest AS build
RUN apt-get update && apt-get install -y locales && localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8
ENV LANG en_US.utf8
RUN apt-get install -y build-essential git zlib1g-dev curl openssl pkg-config libssl-dev
RUN mkdir -p /opt/
RUN cd /opt/ && git clone https://github.com/lh3/miniprot.git && cd /opt/miniprot && make
RUN mkdir -p /opt/bin/ && cp /opt/miniprot/miniprot /opt/bin/
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y
RUN cd /opt/ && git clone https://github.com/cschin/LILRpalooza.git && cd /opt/LILRpalooza/server && . $HOME/.cargo/env && cargo build --release && cp /opt/LILRpalooza/server/target/release/server /opt/bin && cargo clean
RUN cp -a /opt/LILRpalooza/server/ref_data/ /opt/ref_data/
RUN rm -rf /var/lib/apt/lists/*

FROM ubuntu:latest
RUN apt-get update && apt-get install -y locales && localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8
RUN apt-get install -y zlib1g-dev ca-certificates
RUN rm -rf /var/lib/apt/lists/*
ENV LANG en_US.utf8
RUN mkdir -p /opt/ && mkdir -p /opt/bin 
COPY --from=build /opt/ref_data/ /opt/ref_data/
COPY --from=build /opt/miniprot/miniprot /opt/bin/
COPY --from=build /opt/bin/server /opt/bin/
ENTRYPOINT ["/opt/bin/server"]
