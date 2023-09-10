# Pull in ofelia binary from container image because they didn't create
# binaries for the latest release (0.3.7)
FROM mcuadros/ofelia:39bca16 as ofelia

# The container image we'll build to use as is
FROM alpine:3.18

COPY --from=ofelia /usr/bin/ofelia /usr/bin/ofelia

SHELL ["/bin/ash", "-c"]

# We update the CA certificates, add the time zone data for ofelia, and ssh for
# copying over the TLS certificates to the servers
# hadolint disable=DL3018
RUN apk update && \
  apk --no-cache add ca-certificates tzdata openssh && \
  update-ca-certificates && \
  rm -rf /var/cache/apk/*

# Download Lego for ACME TLS certificates
RUN set -eux; \
  version='4.14.0'; \
  arch=$(uname -a); \
  lego_arch='amd64'; \
  temp_dir=$(mktemp -d) && cd "${temp_dir}"; \
  if [ "${arch}" = 'aarch64' ]; then lego_arch='arm64'; fi; \
  wget -q -O lego_checksums.txt "https://github.com/go-acme/lego/releases/download/v${version}/lego_${version}_checksums.txt"; \
  wget -q "https://github.com/go-acme/lego/releases/download/v${version}/lego_v${version}_linux_${lego_arch}.tar.gz"; \
  grep "linux_${lego_arch}\.tar\.gz" 'lego_checksums.txt'  | sha256sum -c - ; \
  tar -x -f "lego_v${version}_linux_${lego_arch}.tar.gz"; \
  mv lego /usr/bin/lego; \
  lego --version; \
  rm -rf "${temp_dir}"
