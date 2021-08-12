FROM ubuntu:20.04
RUN apt-get update && apt-get install -y software-properties-common wget
RUN add-apt-repository ppa:wordops/nginx-wo -uy \
    && apt-get update && apt-get install -y nginx-custom nginx-wo

# forward request and error logs to docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log \
    && ln -sf /dev/stderr /var/log/nginx/error.log \
    # create a docker-entrypoint.d directory
    && mkdir /docker-entrypoint.d

EXPOSE 80

STOPSIGNAL SIGQUIT

CMD ["nginx", "-g", "daemon off;"]
