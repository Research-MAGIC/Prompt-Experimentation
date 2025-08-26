FROM python:3.11-slim

# Install system dependencies including bash
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends \
    git \
    curl \
    build-essential \
    bash \  # Ensure bash is installed
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Create a non-root user WITH BASH AS SHELL
ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
    --shell /bin/bash \  # ADD THIS LINE to set bash as the default shell
    && apt-get update \
    && apt-get install -y sudo \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME

# Remove the manual Node.js installation since the feature will handle it
# (This avoids conflicts between your manual installation and the feature)

# Install Python packages
RUN pip install --upgrade pip
RUN pip install chainforge

# Set working directory
WORKDIR /workspace

# Expose ports
EXPOSE 8000 8001

USER $USERNAME
