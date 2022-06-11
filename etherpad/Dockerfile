# build:
#  docker build --build-arg HTTP_PROXY=http://172.16.0.4:3128/ --tag=etherpad /home/docker/mybuilds/etherpad/
#  docker build --tag=etherpad /home/bedis/containers/etherpad/
# run:
#  docker run -it --rm=true --name=tiny_etherpad --hostname=etherpad etherpad
# debug run:
#  docker run -it --rm=true --expose=80 --env=CONFVER=1 --entrypoint=sh -v /home/docker/myvolumes/haproxytraining/:/mnt/training etherpad

FROM node:18-alpine3.14

ARG ETHERPAD_VER=

ENV DEL_PKGS="openssl" RM_DIRS="/usr/src/* /var/cache/apk/*" PAD_BUILD_DEPENDENCY="openssl openssl-dev pcre pcre-dev zlib zlib-dev"


RUN apk add -U curl openssl git python3 sqlite \
  && mkdir /usr/src \
  && cd /usr/src \
  && echo "Downloading etherpad-${ETHERPAD_VER}.tar.gz" \
  && if [ ! -f etherpad-${ETHERPAD_VER} ]; then \
  curl -L -v https://github.com/ether/etherpad-lite/tarball/${ETHERPAD_VER} -o etherpad-${ETHERPAD_VER}.tar.gz ; \
  fi \
  && tar xzf etherpad-${ETHERPAD_VER}.tar.gz \
  && cd /usr/src/ether-etherpad-lite-*/bin \
  && ./installDeps.sh \
  && apk del make gcc g++ linux-headers ${DEL_PKGS} \
  && cd / \
  #&& mkdir /opt \
  && mv /usr/src/ether-etherpad-lite-* /opt/etherpad \
  && apk del ${DEL_PKGS} \
  && rm -rf ${RM_DIRS}

ADD /start_etherpad.sh /

EXPOSE 9001

ENTRYPOINT /start_etherpad.sh
