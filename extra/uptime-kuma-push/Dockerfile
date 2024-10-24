FROM node@sha256:9d09fa506f5b8465c5221cbd6f980e29ae0ce9a3119e2b9bc0842e6a3f37bb59 AS build
RUN useradd --create-home kuma
USER kuma
WORKDIR /home/kuma
ARG TARGETPLATFORM
COPY --chown=kuma:kuma ./build/ ./build/
COPY --chown=kuma:kuma build.js build.js
RUN node build.js $TARGETPLATFORM

FROM debian:bookworm-slim@sha256:36e591f228bb9b99348f584e83f16e012c33ba5cad44ef5981a1d7c0a93eca22 AS release
RUN useradd --create-home kuma
USER kuma
WORKDIR /home/kuma
COPY --from=build /home/kuma/uptime-kuma-push ./uptime-kuma-push

ENTRYPOINT ["/home/kuma/uptime-kuma-push"]


