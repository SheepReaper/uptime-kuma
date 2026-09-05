FROM node@sha256:f5d1cc40abc10c2843339a2134d07817cf33c405cb16bfd052b0ed790254c3a3 AS build
RUN useradd --create-home kuma
USER kuma
WORKDIR /home/kuma
ARG TARGETPLATFORM
COPY --chown=kuma:kuma ./build/ ./build/
COPY --chown=kuma:kuma build.js build.js
RUN node build.js $TARGETPLATFORM

FROM debian:bookworm-slim@sha256:88200866dfff7ea7f5cbcb6ec7c8a701889efe6fe859fe64d6990e4b07ea4171 AS release
RUN useradd --create-home kuma
USER kuma
WORKDIR /home/kuma
COPY --from=build /home/kuma/uptime-kuma-push ./uptime-kuma-push

ENTRYPOINT ["/home/kuma/uptime-kuma-push"]


