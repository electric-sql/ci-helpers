ARG ELIXIR_VERSION=1.13.4
ARG OTP_VERSION=24.3
ARG DEBIAN_VERSION=bullseye-20210902-slim

ARG BUILDER_IMAGE="hexpm/elixir:${ELIXIR_VERSION}-erlang-${OTP_VERSION}-debian-${DEBIAN_VERSION}"

FROM ${BUILDER_IMAGE}
LABEL maintainer="dev@electric-sql.com"
RUN apt-get update -y && \
    apt-get install -y build-essential git curl && \
    apt-get clean && \
    rm -f /var/lib/apt/lists/*_*

ENV MIX_ENV=prod
RUN mix local.hex --force && mix local.rebar --force