FROM nginx

COPY ./docker/nginx/site.conf /etc/nginx/conf.d/default.conf

RUN mkdir -p /app/public
COPY ./public/ /app/public/

USER nginx

CMD ["nginx"]
