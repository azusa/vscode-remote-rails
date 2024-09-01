ARG VARIANT=1.1.9-3.3-bullseye
FROM mcr.microsoft.com/devcontainers/ruby:${VARIANT}

# Install Rails
RUN gem install rails webdrivers

# Default value to allow debug server to serve content over GitHub Codespace's port forwarding service
# The value is a comma-separated list of allowed domains 
ENV RAILS_DEVELOPMENT_HOSTS=".githubpreview.dev,.app.github.dev"

ENV PYTHON=/usr/bin/python3

# [Choice] Node.js version: lts/*, 16, 14, 12, 10
ARG NODE_VERSION="lts/*"
RUN su vscode -c "source /usr/local/share/nvm/nvm.sh && nvm install ${NODE_VERSION} 2>&1"


RUN apt-get update
 
RUN export DEBIAN_FRONTEND=noninteractive && apt-get -y install --no-install-recommends python3

RUN mkdir -p /workspace/vendor/.cache

RUN sudo gem install ruby-lsp
