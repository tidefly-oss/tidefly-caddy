FROM caddy:2-builder AS builder

RUN xcaddy build \
    --with github.com/mholt/caddy-l4 \
    --with github.com/mholt/caddy-ratelimit \
    --with github.com/hslatman/caddy-crowdsec-bouncer \
    --with github.com/corazawaf/coraza-caddy \
    --output /usr/bin/caddy

RUN /usr/bin/caddy list-modules | grep -E "layer4|ratelimit"

FROM caddy:2-alpine

COPY --from=builder /usr/bin/caddy /usr/bin/caddy

EXPOSE 80 443 2019

HEALTHCHECK --interval=10s --timeout=3s --start-period=10s --retries=3 \
    CMD wget -qO- http://localhost:2019/ || exit 1

ENTRYPOINT ["/usr/bin/caddy"]
CMD ["run"]