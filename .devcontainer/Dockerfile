FROM ghcr.io/graalvm/jdk-community:25i3-25.0.4.1-ol10

RUN microdnf install -y \
        ca-certificates \
        curl \
        git \
        jq \
        unzip \
        zlib \
    && microdnf clean all

RUN useradd --create-home --shell /bin/bash vscode

COPY versions.json /tmp/versions.json

RUN PROTOS_VERSION="$(jq -r '.protos.version' /tmp/versions.json)" \
    && PROTOS_RELEASE_TAG="$(jq -r '.protos.releaseTag' /tmp/versions.json)" \
    && PROTOS_ASSET="$(jq -r '.protos.asset' /tmp/versions.json)" \
    && PROTOS_SHA256="$(jq -r '.protos.sha256' /tmp/versions.json)" \
    && test -n "$PROTOS_VERSION" \
    && test -n "$PROTOS_RELEASE_TAG" \
    && test -n "$PROTOS_ASSET" \
    && test -n "$PROTOS_SHA256" \
    && test "$PROTOS_RELEASE_TAG" = "v$PROTOS_VERSION" \
    && test "$PROTOS_ASSET" = "protos-${PROTOS_VERSION}-native-linux-x86_64.zip" \
    && mkdir -p "/opt/protos/$PROTOS_VERSION" \
    && curl -fL \
        -o "/tmp/$PROTOS_ASSET" \
        "https://github.com/guillermomolina/protos/releases/download/$PROTOS_RELEASE_TAG/$PROTOS_ASSET" \
    && echo "$PROTOS_SHA256  /tmp/$PROTOS_ASSET" | sha256sum -c - \
    && unzip -q "/tmp/$PROTOS_ASSET" -d "/tmp/protos-extracted" \
    && EXTRACTED_ROOT="/tmp/protos-extracted/protos-${PROTOS_VERSION}-native-linux-x86_64" \
    && test -x "$EXTRACTED_ROOT/bin/protos" \
    && cp -a "$EXTRACTED_ROOT/." "/opt/protos/$PROTOS_VERSION/" \
    && printf '#!/bin/sh\nexec "/opt/protos/%s/bin/protos" "$@"\n' "$PROTOS_VERSION" \
        > /usr/local/bin/protos \
    && chmod 0755 /usr/local/bin/protos \
    && rm -rf "/tmp/$PROTOS_ASSET" /tmp/protos-extracted /tmp/versions.json \
    && chown -R vscode:vscode "/opt/protos/$PROTOS_VERSION"

ENV PATH="/usr/local/bin:${PATH}"

WORKDIR /workspaces/protos-devcontainer

USER vscode
