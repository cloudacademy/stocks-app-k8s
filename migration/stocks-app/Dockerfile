FROM node:16.15-alpine AS builder
USER node
RUN mkdir -p /home/node/stocks-app
WORKDIR /home/node/stocks-app
COPY --chown=node . .
RUN yarn install
RUN yarn build

FROM nginx:1.20

LABEL io.k8s.description="Platform for serving static HTML files" \
    io.k8s.display-name="Nginx 1.20"

COPY --from=builder /home/node/stocks-app/build /usr/share/nginx/html/
COPY .env /usr/share/nginx/html/
COPY env-config.js /usr/share/nginx/html/

COPY conf/nginx.conf /etc/nginx/nginx.conf
COPY conf/conf.d/default.conf.template /tmp
COPY conf/conf.d/default.conf /etc/nginx/conf.d/default.conf

RUN chown -R nginx:nginx /usr/share/nginx/html && chmod -R 755 /usr/share/nginx/html && \
        chown -R nginx:nginx /var/cache/nginx && \
        chown -R nginx:nginx /var/log/nginx && \
        chown -R nginx:nginx /etc/nginx/conf.d

RUN touch /var/run/nginx.pid && \
        chown -R nginx:nginx /var/run/nginx.pid

COPY env.sh /tmp
RUN chmod +x /tmp/env.sh

USER nginx
EXPOSE 8080

CMD ["/bin/bash", "-c", "cd /usr/share/nginx/html && /tmp/env.sh && nginx -g \"daemon off;\""]