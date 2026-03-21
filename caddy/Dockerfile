FROM caddy:2-builder AS builder

RUN xcaddy build \
    --with github.com/mholt/caddy-l4 \
    --with github.com/mholt/caddy-ratelimit

FROM caddy:2

COPY --from=builder /usr/bin/caddy /usr/bin/caddy

RUN caddy list-modules | grep -E "layer4|ratelimit"

EXPOSE 80 443 2019

CMD ["caddy", "run", "--config", "/dev/null", "--adapter", "caddyfile"]