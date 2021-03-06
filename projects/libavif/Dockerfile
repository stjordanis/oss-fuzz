# Copyright 2020 Google Inc.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#      http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#
################################################################################

FROM gcr.io/oss-fuzz-base/base-builder
MAINTAINER joedrago@gmail.com

ADD bionic.list /etc/apt/sources.list.d/bionic.list
ADD nasm_apt.pin /etc/apt/preferences

RUN apt-get update && \
    apt-get install --no-install-recommends -y curl python3-pip python3-setuptools python3-wheel cmake git && \
    pip3 install meson ninja

RUN git clone --depth 1 https://github.com/AOMediaCodec/libavif.git libavif
WORKDIR libavif

RUN curl -L https://download.videolan.org/contrib/nasm/nasm-2.14.tar.gz | tar xvz
RUN cd nasm-2.14 && ./configure && make -j2 && ln -s `pwd`/nasm /usr/bin/nasm && cd ..
RUN nasm --version

COPY build.sh avif_decode_fuzzer.cc avif_decode_seed_corpus.zip $SRC/
