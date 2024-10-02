# [Choice] Alpine version: 3.16, 3.15, 3.14, 3.13
ARG VARIANT=3.16
FROM alpine:${VARIANT}

# [Option] Install zsh
ARG INSTALL_ZSH="true"

# Install needed packages and setup non-root user. Use a separate RUN statement to add your own dependencies.
ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID
COPY library-scripts/*.sh /tmp/library-scripts/
RUN apk update && ash /tmp/library-scripts/common-alpine.sh "${INSTALL_ZSH}" "${USERNAME}" "${USER_UID}" "${USER_GID}" && rm -rf /tmp/library-scripts

# Install Docker and Docker Compose
RUN apk add --no-cache \
    docker \
    docker-compose \
    && rc-update add docker boot

# Switch to non-root user
USER ${USERNAME}

# (Optional) Set the working directory
WORKDIR /home/${USERNAME}
