FROM nginx:alpine 
COPY nginx.conf /etc/nginx/conf.d/default.conf
RUN mkdir -p /var/www/html
COPY wwwroot /var/www/html
WORKDIR /var/www/html
RUN wget https://use.fontawesome.com/releases/v6.1.1/fontawesome-free-6.1.1-web.zip -O fontawesome-free-6.1.1-web.zip && \
  unzip fontawesome-free-6.1.1-web.zip && \
  mv fontawesome-free-6.1.1-web fontawesome && \
  rm fontawesome-free-6.1.1-web.zip
