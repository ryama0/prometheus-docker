ARG SOURCE

FROM ${SOURCE} AS build-env
ARG VERSION
ARG ARCH
RUN apt-get update && \
    apt-get install -y wget && \
    wget https://github.com/prometheus/alertmanager/releases/download/v${VERSION}/alertmanager-${VERSION}.linux-${ARCH}.tar.gz && \
    tar xzvf alertmanager-${VERSION}.linux-${ARCH}.tar.gz -C /

FROM ${SOURCE}
ARG VERSION
ARG ARCH
RUN apt-get update && \
    apt-get install -y --no-install-recommends ca-certificates && \
    rm -rf /var/lib/apt/lists/*
COPY --from=build-env /alertmanager-${VERSION}.linux-${ARCH}/amtool /bin/amtool
COPY --from=build-env /alertmanager-${VERSION}.linux-${ARCH}/alertmanager /bin/alertmanager
COPY --from=build-env /alertmanager-${VERSION}.linux-${ARCH}/alertmanager /etc/alertmanager/alertmanager.yml

EXPOSE 9093
VOLUME ["/alertmanager"]
WORKDIR /alertmanager
ENTRYPOINT [ "/bin/alertmanager" ]
CMD [ "--config.file=/etc/alertmanager/alertmanager.yml", \
      "--storage.path=/alertmanager" ]
