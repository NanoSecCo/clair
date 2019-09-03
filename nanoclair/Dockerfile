# Copyright 2017 clair authors
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

#FROM golang:1.10-alpine
FROM alpine:3.10

VOLUME /config
EXPOSE 6060 6061

#ADD .   /go/src/github.com/coreos/clair/
#WORKDIR /go/src/github.com/coreos/clair/
COPY config.example.yaml /opt/nanoclair/config/
COPY clair /opt/nanoclair/bin/
WORKDIR /opt/nanoclair/

#RUN apk add --no-cache git rpm xz dumb-init && \
#    export CLAIR_VERSION=$(git describe --always --tags --dirty) && \
#    go install -ldflags "-X github.com/coreos/clair/pkg/version.Version=$CLAIR_VERSION" -v github.com/coreos/clair/cmd/clair && \
#    mv /go/bin/clair /clair && \
#    rm -rf /go /usr/local/go
RUN apk add --no-cache git rpm xz dumb-init && \
    mkdir /lib64 && ln -s /lib/libc.musl-x86_64.so.1 /lib64/ld-linux-x86-64.so.2

#ENTRYPOINT ["/usr/bin/dumb-init", "--", "/clair"]
ENTRYPOINT ["/usr/bin/dumb-init", "--", "bin/clair", "-config", "config/config.example.yaml"]
#ENTRYPOINT ["/usr/bin/dumb-init", "--", "bin/clair", "-config", "config/config.example.yaml", "-log-level", "debug"]
#ENTRYPOINT ["/usr/bin/dumb-init", "--", "sleep", "10000000"]

