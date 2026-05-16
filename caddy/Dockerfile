FROM caddy:2-builder AS builder

RUN xcaddy build \
    --with github.com/mholt/caddy-l4 \
    --with github.com/mholt/caddy-ratelimit \
    --output /usr/bin/caddy

# Verify modules during build (nicht im finalen Image)
RUN /usr/bin/caddy list-modules | grep -E "layer4|ratelimit"

FROM gcr.io/distroless/static-debian12

COPY --from=builder /usr/bin/caddy /usr/bin/caddy

EXPOSE 80 443 2019

ENTRYPOINT ["/usr/bin/caddy"]
CMD ["run", "--config", "/dev/null", "--adapter", "caddyfile"]