FROM nginx:alpine

ARG ROOT_DOMAIN=${ROOT_DOMAIN}
ARG SSL_CERTIFICATE=${SSL_CERTIFICATE}
ENV ROOT_DOMAIN=${ROOT_DOMAIN}
ENV SSL_CERTIFICATE=${SSL_CERTIFICATE}

RUN apk update && \
    apk add --no-cache \
    openrc \
    bind-tools \
    bash \
    vim \
    openssl \
    cronie \
    git

COPY nginx.conf /etc/nginx/nginx.conf
COPY conf.d /etc/nginx/tmp/conf.d
COPY scripts /home/user/scripts

WORKDIR /home/user/scripts
RUN chmod +x *
RUN ./init.sh

EXPOSE 80
EXPOSE 443

ENTRYPOINT ["sh", "-c", "crond -s & nginx -g 'daemon off;'"]
