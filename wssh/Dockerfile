FROM python:3-alpine

RUN \
  apk add --no-cache libc-dev libffi-dev gcc git && \
  mkdir /code && cd /code && \
  git clone https://github.com/huashengdun/webssh && cd webssh && \
  pip install -r requirements.txt --no-cache-dir && \
  apk del gcc libc-dev libffi-dev && \
  addgroup webssh && \
  adduser -Ss /bin/false -g webssh webssh && \
  chown -R webssh:webssh /code/webssh

COPY index.html /code/webssh/webssh/templates/index.html

WORKDIR /code/webssh
EXPOSE 8888/tcp
USER webssh
CMD ["python", "run.py", "--redirect", "false", "--fbidhttp", "false", "--origin", "*", "--debug", "true", "--xsrf", "false"]