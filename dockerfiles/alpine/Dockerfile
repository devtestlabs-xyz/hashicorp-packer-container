# Official Alpine Linux image
ARG BASE_IMAGE_VERSION
FROM alpine:${BASE_IMAGE_VERSION}

# Build arguments
# Values set by Github Actions
ARG PACKER_VERSION
ARG PACKER_SHA256SUM
ARG VCS_URL
ARG VCS_REF
ARG BUILD_DATETIME
ARG IMAGE_LONG_VERSION

# ENV PACKER_VERSION=1.6.0 
# ENV PACKER_SHA256SUM=a678c995cb8dc232db3353881723793da5acc15857a807d96c52e96e671309d9

# ENV VIRT_APK_PACKAGES \
#   git \
#   wget 

ENV APK_PACKAGES \
  openssl \
  bash \
  ca-certificates 

ADD https://releases.hashicorp.com/packer/${PACKER_VERSION}/packer_${PACKER_VERSION}_linux_amd64.zip ./
ADD https://releases.hashicorp.com/packer/${PACKER_VERSION}/packer_${PACKER_VERSION}_SHA256SUMS ./

RUN set -x \
    && \
    env \
    # && echo "===> Temporarily installing APKs (virtual packages)..." \
    # && apk add --no-cache --virtual .build-deps ${VIRT_APK_PACKAGES} \
    && \
    echo "==> Upgrading apk and system..." \
    && apk update && apk upgrade \
    && \
    echo "==> Installing required APKs..." \
    && apk add --no-cache ${APK_PACKAGES}

RUN sed -i '/.*linux_amd64.zip/!d' packer_${PACKER_VERSION}_SHA256SUMS \
    && sha256sum -cs packer_${PACKER_VERSION}_SHA256SUMS \
    && unzip packer_${PACKER_VERSION}_linux_amd64.zip -d /bin \
    && rm -f packer_${PACKER_VERSION}_linux_amd64.zip

RUN echo "===> Cleaning up..." \
    # && apk del .build-deps \
    && unset http_proxy https_proxy

ENTRYPOINT ["/bin/packer"]

# Labels
# http://label-schema.org/rc1/ namespace labels
LABEL maintainer="Ryan Craig <ryan.s.craig@gmail.com>"

LABEL org.label-schema.schema-version="1.0"
LABEL org.label-schema.build-date=${BUILD_DATETIME}
LABEL org.label-schema.name="devtestlabs/packer"
LABEL org.label-schema.description="Hashicorp Packer"
#LABEL org.label-schema.url=$ORG_WEB_URL
LABEL org.label-schema.vcs-url=${VCS_URL}
LABEL org.label-schema.vcs-ref=${VCS_REF}
LABEL org.label-schema.vendor="devtestlabs.xyz"
LABEL org.label-schema.version=${IMAGE_LONG_VERSION}