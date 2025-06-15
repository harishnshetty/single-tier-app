FROM nginx:alpine

# Remove default HTML and conf
RUN rm -rf /usr/share/nginx/html/* /etc/nginx/conf.d/default.conf

# Copy HTML and template conf
COPY index.html /usr/share/nginx/html/index.html
COPY default.conf /etc/nginx/templates/default.conf.template

# Enable envsubst-based conf rendering
ENV NGINX_ENVSUBST_TEMPLATE_SUFFIX=.template
ENV NGINX_ENVSUBST_OUTPUT_DIR=/etc/nginx/conf.d

CMD ["/docker-entrypoint.sh", "nginx", "-g", "daemon off;"]
