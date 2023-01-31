FROM debian:11-slim as builder

WORKDIR /app

RUN apt-get update \
  && apt-get install -y git gcc g++ libpq-dev make automake libtool pkg-config

ARG SYSBENCH_COMMIT

RUN git clone https://github.com/akopytov/sysbench.git \
  && cd sysbench \
  && git checkout ${SYSBENCH_COMMIT} \
  && ./autogen.sh \
  && ./configure --without-mysql --with-pgsql \
  && make \
  && make install \
  && make clean

FROM debian:11-slim
RUN apt-get update && apt-get install -y libpq-dev

COPY --from=builder /usr/local/bin/sysbench /usr/local/bin/sysbench
