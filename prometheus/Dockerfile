FROM ubuntu:cosmic

RUN apt-get update &&\
    apt-get install -y prometheus --no-install-recommends && \
    mkdir -p /prometheus && \
    chown -R nobody:nogroup /etc/prometheus /prometheus

USER nobody
EXPOSE 9090
VOLUME [ "/prometheus" ]
WORKDIR "/prometheus"
ENTRYPOINT [ "/usr/bin/prometheus" ]
CMD [ "--config.file=/etc/prometheus/prometheus.yml", \
      "--storage.tsdb.path=/prometheus", \
      "--web.console.libraries=/etc/prometheus/console_libraries", \
      "--web.console.templates=/etc/prometheus/consoles" ]
