FROM ubuntu:cosmic

RUN apt-get update &&\
    apt-get install -y prometheus-alertmanager --no-install-recommends && \
    mkdir -p /alertmanager && \
    chown -R nobody:nogroup /etc/prometheus /alertmanager && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

USER nobody
EXPOSE 9093
VOLUME [ "/prometheus" ]
WORKDIR "/prometheus"
ENTRYPOINT [ "/usr/bin/prometheus-alertmanager" ]
CMD [ "-config.file=/etc/prometheus/alertmanager.yml", \
      "-storage.path=/alertmanager" ]
