FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y \
    curl zip unzip bash ca-certificates openjdk-21-jdk \
    && rm -rf /var/lib/apt/lists/*

ENV JAVA_HOME=/usr/lib/jvm/java-21-openjdk-amd64
ENV PATH="$JAVA_HOME/bin:$PATH"

RUN curl -L -o /usr/local/bin/pkl \
    https://github.com/apple/pkl/releases/download/0.30.0/pkl-linux-amd64 \
    && chmod +x /usr/local/bin/pkl

# Defaults, but Dev Containers will override at runtime
ARG UID=1000
ARG GID=1000

RUN groupadd -g ${GID} devgroup \
    && useradd -m -u ${UID} -g ${GID} -s /bin/bash devuser

WORKDIR /workspace
USER devuser

ENTRYPOINT ["pkl"]
