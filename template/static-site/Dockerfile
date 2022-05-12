FROM --platform=${BUILDPLATFORM:-linux/amd64} ghcr.io/openfaas/of-watchdog:0.9.6 AS watchdog

ARG BUILDPLATFORM

FROM scratch
COPY --from=watchdog /fwatchdog /fwatchdog

ENV mode="static"
ENV static_path="/static"

WORKDIR /static
COPY ./function .

HEALTHCHECK --interval=3s CMD [ -e /tmp/.lock ] || exit 1

USER 1000
CMD ["/fwatchdog"]
