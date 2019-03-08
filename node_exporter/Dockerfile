FROM ubuntu:cosmic

RUN apt-get update &&\
    apt-get install -y prometheus-node-exporter --no-install-recommends && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

USER nobody
EXPOSE 9100
ENTRYPOINT [ "/usr/bin/prometheus-node-exporter" ]
