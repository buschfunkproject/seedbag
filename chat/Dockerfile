FROM golang:1.18-buster AS build-env

RUN cd /root && git clone https://github.com/shazow/ssh-chat
WORKDIR /root/ssh-chat

RUN git checkout 621ae1b && \
  make build

#RUN go install github.com/shazow/ssh-chat@latest

FROM debian:bullseye

RUN apt-get update && apt-get install -y \
  ssh \
  && rm -rf /var/lib/apt/lists/*

EXPOSE 9004

RUN groupadd \
  --gid 1000 \
  chat && \
  useradd \
  --home-dir /opt/chat \
  --comment "ssh chat" \
  --gid chat \
  --create-home \
  --no-user-group \
  --uid 1000 \
  --shell /bin/bash \
  chat

COPY --from=build-env /root/ssh-chat/ssh-chat /opt/chat/ssh-chat
RUN chown -R \
  chat:chat /opt/chat

WORKDIR /opt/chat
USER chat
RUN ssh-keygen -t rsa -N '' -f /opt/chat/.ssh/id_rsa
CMD [ "/opt/chat/ssh-chat", "--bind", "\":9004\"", "--verbose"]
#CMD ["tail", "-f", "/dev/null"]