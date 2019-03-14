ARG SOURCE

FROM ${SOURCE} AS build-env
ARG VERSION
ARG ARCH
RUN apt-get update && \
    apt-get install -y wget && \
    mkdir /prometheus && \
    wget https://github.com/prometheus/node_exporter/releases/download/v${VERSION}/node_exporter-${VERSION}.linux-${ARCH}.tar.gz && \
    tar xzvf node_exporter-${VERSION}.linux-${ARCH}.tar.gz -C /

FROM ${SOURCE}
ARG VERSION
ARG ARCH
COPY --from=build-env /node_exporter-${VERSION}.linux-${ARCH}/node_exporter /bin/node_exporter

EXPOSE 9100
ENTRYPOINT [ "/bin/node_exporter" ]
