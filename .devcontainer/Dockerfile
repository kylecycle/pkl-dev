FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

# Install dependencies
RUN apt-get update && apt-get install -y \
    curl zip unzip bash ca-certificates openjdk-21-jdk \
    && rm -rf /var/lib/apt/lists/*

# Set JAVA_HOME for PKL
ENV JAVA_HOME=/usr/lib/jvm/java-21-openjdk-amd64
ENV PATH="$JAVA_HOME/bin:$PATH"

# Install PKL
#RUN curl -fsSL https://pkl-lang.org/install.sh | bash
RUN curl -L -o /usr/local/bin/pkl 'https://github.com/apple/pkl/releases/download/0.30.0/pkl-linux-amd64' \
    && chmod +x /usr/local/bin/pkl

# Add PKL to PATH (if not added by script)
ENV PATH="/root/.pkl/bin:${PATH}"

# Create a user that will match the host UID/GID at runtime
# Use placeholder values; we'll override USER with devcontainer.json
ARG DEVUSER=devuser
ARG DEVGROUP=devgroup
ARG UID=1000
ARG GID=1000

RUN groupadd -g $GID $DEVGROUP \
    && useradd -m -u $UID -g $GID -s /bin/bash $DEVUSER \
    && echo "$DEVUSER ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers


# Set working directory
WORKDIR /workspace

# Default user will be overridden by devcontainer.json
USER $DEVUSER

CMD ["/bin/bash"]
