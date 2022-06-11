FROM nginx:alpine 
COPY nginx.conf /etc/nginx/conf.d/default.conf
RUN mkdir -p /var/www/html
COPY wwwroot /var/www/html
