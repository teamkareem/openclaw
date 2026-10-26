FROM node:22-bookworm-slim@sha256:de170b39439eb0e5a3444ad7d60b015614a381e10fecae2e30ec9e735122f38d

RUN set -eux; \
  for attempt in 1 2 3; do \
    if apt-get update -o Acquire::Retries=3; then break; fi; \
    echo "apt-get update failed (attempt ${attempt})" >&2; \
    if [ "${attempt}" -eq 3 ]; then exit 1; fi; \
    sleep 3; \
  done; \
  apt-get -o Acquire::Retries=3 install -y --no-install-recommends \
    bash \
    ca-certificates \
    curl \
    git \
    g++ \
    make \
    python3 \
    sudo \
  && rm -rf /var/lib/apt/lists/*

COPY install-sh-common/cli-verify.sh /usr/local/install-sh-common/cli-verify.sh
COPY install-sh-smoke/run.sh /usr/local/bin/openclaw-install-smoke
RUN chmod +x /usr/local/bin/openclaw-install-smoke

ENTRYPOINT ["/usr/local/bin/openclaw-install-smoke"]
