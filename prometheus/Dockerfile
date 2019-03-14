ARG SOURCE

FROM ${SOURCE} AS build-env
ARG VERSION
ARG ARCH
RUN apt-get update && \
    apt-get install -y wget && \
    wget https://github.com/prometheus/prometheus/releases/download/v${VERSION}/prometheus-${VERSION}.linux-${ARCH}.tar.gz && \
    tar xzvf prometheus-${VERSION}.linux-${ARCH}.tar.gz -C /

FROM ${SOURCE}
ARG VERSION
ARG ARCH
COPY --from=build-env /prometheus-${VERSION}.linux-${ARCH}/prometheus /bin/prometheus
COPY --from=build-env /prometheus-${VERSION}.linux-${ARCH}/promtool /bin/promtool
COPY --from=build-env /prometheus-${VERSION}.linux-${ARCH}/prometheus.yml /etc/prometheus/prometheus.yml
COPY --from=build-env /prometheus-${VERSION}.linux-${ARCH}/console_libraries/ /usr/share/prometheus/console_libraries/
COPY --from=build-env /prometheus-${VERSION}.linux-${ARCH}/consoles/ /usr/share/prometheus/consoles/

EXPOSE 9090
VOLUME [ "/prometheus" ]
WORKDIR "/prometheus"
ENTRYPOINT [ "/bin/prometheus" ]
CMD [ "--config.file=/etc/prometheus/prometheus.yml", \
      "--storage.tsdb.path=/prometheus", \
      "--web.console.libraries=/etc/prometheus/console_libraries", \
      "--web.console.templates=/etc/prometheus/consoles" ]
