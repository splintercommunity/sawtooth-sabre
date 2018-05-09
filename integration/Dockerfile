# Copyright 2018 Cargill Incorporated
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

FROM ubuntu:xenial

RUN echo "deb [arch=amd64] http://repo.sawtooth.me/ubuntu/ci xenial universe" >> /etc/apt/sources.list \
 && apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 8AA7AF1F1091A5FD \
 && apt-get update \
 && apt-get install -y -q --allow-downgrades \
    build-essential \
    git \
    libffi-dev \
    libssl-dev \
    libzmq3-dev \
    python3-pip

RUN apt-get update && apt-get install -y -q --no-install-recommends \
    curl \
 && curl -s -S -o /tmp/setup-node.sh https://deb.nodesource.com/setup_6.x

RUN curl https://sh.rustup.rs -sSf > /usr/bin/rustup-init \
 &&  chmod +x /usr/bin/rustup-init \
 && rustup-init -y

ENV PATH=$PATH:/protoc3/bin:/root/.cargo/bin \
 CARGO_INCREMENTAL=0

RUN rustup toolchain add nightly \
  && rustup update \
  && rustup target add wasm32-unknown-unknown --toolchain nightly \
  && rustup default nightly

WORKDIR /project/example/intkey_multiply/processor