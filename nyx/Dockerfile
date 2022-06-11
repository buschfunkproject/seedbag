FROM golang:1.18-buster AS build-env

RUN cd /root && git clone https://github.com/rls-moe/nyx
WORKDIR /root/nyx

RUN go build -o $GOPATH/bin/nyx

FROM debian:bullseye

EXPOSE 8080

RUN groupadd \
  --gid 1000 \
  nyx && \
  useradd \
  --home-dir /opt/nyx \
  --comment "Nyx Board" \
  --gid nyx \
  --create-home \
  --no-user-group \
  --uid 1000 \
  --shell /bin/bash \
  nyx

COPY --from=build-env /go/bin/nyx /opt/nyx/nyx
COPY --from=build-env /root/nyx/config.example.yml /opt/nyx/config.yml
COPY config.yml /opt/nyx/config.yml
RUN chown -R \
  nyx:nyx /opt/nyx

WORKDIR /opt/nyx
USER nyx
CMD [ "/opt/nyx/nyx" ]