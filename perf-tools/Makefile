#
# Licensed to the Apache Software Foundation (ASF) under one
# or more contributor license agreements.  See the NOTICE file
# distributed with this work for additional information
# regarding copyright ownership.  The ASF licenses this file
# to you under the Apache License, Version 2.0 (the
# "License"); you may not use this file except in compliance
# with the License.  You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

.PHONY: build clean

TARGET_DIR ?= target
BINARY_DIR ?= perf-tools-bin
BINARY ?= perf-tools

GOOS ?= $(shell go env GOOS)
GOARCH ?= $(shell go env GOARCH)

build: clean
	@mkdir ${TARGET_DIR}
	@mkdir ${TARGET_DIR}/${BINARY_DIR}
	@echo "[Action] mkdir target and bin directory"
	@CGO_ENABLED=0 GOOS=${GOOS} GOARCH=${GOARCH} go build -o ${TARGET_DIR}/${BINARY_DIR}/${BINARY} .
	@echo "[Action] build binary"
	@cp conf.yaml ${TARGET_DIR}/${BINARY_DIR}
	@echo "[Action] copy binary and conf file to binary directory"
	@tar -zcvf ${TARGET_DIR}/${BINARY_DIR}.tar.gz -C ${TARGET_DIR} ${BINARY_DIR}
	@echo "[Action] generate binary package: ${TARGET_DIR}/${BINARY_DIR}.tar.gz"

clean:
	@if [ -d "${TARGET_DIR}" ] ; then rm -rf ${TARGET_DIR} && echo "[Action] cleaned target directory" ; fi
