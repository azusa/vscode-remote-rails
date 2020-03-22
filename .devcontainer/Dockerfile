#-----------------------------------------------------------------------------------------
# Copyright (c) Microsoft Corporation. All rights reserved.
# Licensed under the MIT License. See LICENSE in the project root for license information.
#-----------------------------------------------------------------------------------------

FROM ruby:2.6-buster

# Or your actual UID, GID on Linux if not the default 1000
ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

# Configure apt
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update \
    # ① apt-utilsのインストール
    && apt-get -y install --no-install-recommends apt-utils dialog 2>&1 \
    #
    # ② 必要なパッケージのインストール
    && apt-get -y install curl git procps lsb-release \
    # ③ Ruby on Railsのビルドに必要なパッケージのインストール
    build-essential libsqlite3-dev nodejs sqlite3  \
    # ④ ユーザーの追加
    && groupadd --gid $USER_GID $USERNAME \
    && useradd -s /bin/bash --uid $USER_UID --gid $USER_GID -m $USERNAME \
    && apt-get install -y sudo \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME \
    # ⑤ 開発環境のセットアップ
    && gem install rails bundler solargraph \
    && ln -s /usr/local/bundle/bin/solargraph /usr/local/bin/solargraph \
    && curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -  \
    && echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list \
    && apt-get update && sudo apt-get install yarn \
    #
    # Clean up
    && apt-get autoremove -y \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/*

ENV DEBIAN_FRONTEND=
