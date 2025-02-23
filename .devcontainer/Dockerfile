FROM golang:1.24

ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

# Create the user
RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
    && apt-get update \
    && apt-get install -y sudo \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME

# Install additional tools
RUN apt-get update && apt-get install -y \
    git \
    curl \
    vim \
    wget \
    zip \
    unzip \
    && rm -rf /var/lib/apt/lists/*

# Install Go tools
RUN go install golang.org/x/tools/gopls@latest \
    && go install github.com/go-delve/delve/cmd/dlv@latest \
    && go install github.com/golangci/golangci-lint/cmd/golangci-lint@latest

# Switch to vscode user
USER $USERNAME

# Set the default shell to bash
ENV SHELL /bin/bash