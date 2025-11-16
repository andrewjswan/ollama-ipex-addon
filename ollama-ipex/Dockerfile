### Build Ollama IPEX

# Use phusion/baseimage as base image. To make your builds reproducible, make
# sure you lock down to a specific version, not to `latest`!
# See https://github.com/phusion/baseimage-docker/releases for
# a list of version numbers.
ARG BUILD_FROM
FROM ${BUILD_FROM}

ENV DEBIAN_FRONTEND=noninteractive

# Build arguments
ARG BUILD_ARCH
ARG BUILD_DATE
ARG BUILD_DESCRIPTION
ARG BUILD_NAME
ARG BUILD_REF
ARG BUILD_REPOSITORY
ARG BUILD_VERSION

# Add Label
LABEL \
    io.hass.name="${BUILD_NAME}" \
    io.hass.description="${BUILD_DESCRIPTION}" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="Andrew J.Swan <andrewjswan@addons.community>" \
    org.opencontainers.image.title="${BUILD_NAME}" \
    org.opencontainers.image.description="${BUILD_DESCRIPTION}" \
    org.opencontainers.image.vendor="Andrew J.Swan" \
    org.opencontainers.image.authors="Andrew J.Swan <andrewjswan@addons.community>" \
    org.opencontainers.image.licenses="MIT" \
    org.opencontainers.image.created=${BUILD_DATE} \
    org.opencontainers.image.revision=${BUILD_REF} \
    org.opencontainers.image.version=${BUILD_VERSION} \
    org.opencontainers.image.source="https://github.com/${BUILD_REPOSITORY}" \
    org.opencontainers.image.documentation="https://github.com/${BUILD_REPOSITORY}/blob/master/README.md"

# Use baseimage-docker's init system.
CMD ["/sbin/my_init"]

# Base packages
RUN \
    apt update \
    && apt install --no-install-recommends -q -y \
       software-properties-common \
       ca-certificates \
       wget \
       ocl-icd-libopencl1

# Intel GPU compute user-space drivers
RUN \
    mkdir -p /tmp/gpu && \
    cd /tmp/gpu && \
    echo "Downloading oneAPI Level Zero Loader v1.26.0..." && \
    wget https://github.com/oneapi-src/level-zero/releases/download/v1.26.0/level-zero_1.26.0+u24.04_amd64.deb && \
    echo "Downloading Intel Graphics Compiler v2.20.3..." && \
    wget https://github.com/intel/intel-graphics-compiler/releases/download/v2.20.3/intel-igc-core-2_2.20.3+19972_amd64.deb && \
    wget https://github.com/intel/intel-graphics-compiler/releases/download/v2.20.3/intel-igc-opencl-2_2.20.3+19972_amd64.deb && \
    echo "Downloading Intel Compute Runtime v25.40..." && \
    wget https://github.com/intel/compute-runtime/releases/download/25.40.35563.4/intel-ocloc_25.40.35563.4-0_amd64.deb && \
    wget https://github.com/intel/compute-runtime/releases/download/25.40.35563.4/intel-opencl-icd_25.40.35563.4-0_amd64.deb && \
    wget https://github.com/intel/compute-runtime/releases/download/25.40.35563.4/libigdgmm12_22.8.2_amd64.deb && \
    wget https://github.com/intel/compute-runtime/releases/download/25.40.35563.4/libze-intel-gpu1_25.40.35563.4-0_amd64.deb && \
    dpkg -i --force-all *.deb && \
    rm *.deb

# Install Ollama Portable Zip
ARG IPEXLLM_RELEASE_REPO=ipex-llm/ipex-llm
ARG IPEXLLM_RELEASE_VERSON=v2.3.0-nightly
ARG IPEXLLM_PORTABLE_ZIP_FILENAME=ollama-ipex-llm-2.3.0b20250725-ubuntu.tgz
RUN \
    cd / && \
    echo "Downloading Ollama Portable on Intel GPU with IPEX-LLM..." && \
    wget https://github.com/${IPEXLLM_RELEASE_REPO}/releases/download/${IPEXLLM_RELEASE_VERSON}/${IPEXLLM_PORTABLE_ZIP_FILENAME} && \
    tar xvf ${IPEXLLM_PORTABLE_ZIP_FILENAME} --strip-components=1 -C / && \
    rm ${IPEXLLM_PORTABLE_ZIP_FILENAME}

# Clean up APT when done.
RUN \
    apt-get clean \
    && rm -fr \
       /tmp/* \
       /var/tmp/* \
       /var/cache/* \
       /var/lib/apt/lists/* \
       /var/log/*.log \
       /var/log/apt

WORKDIR /

# Start Ollama
ENV OLLAMA_HOST=0.0.0.0:11434
ENV no_proxy=localhost,127.0.0.1

EXPOSE 11434

ENTRYPOINT ["./ollama"]
CMD ["serve"]
