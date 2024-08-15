#
# Copyright 2019-2024 Open Text.
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

ARG DOTNET_IMAGE
FROM $DOTNET_IMAGE

# Copy in zypper repo key
COPY dev_zypper_repo_key.pub .

RUN zypper -n addrepo https://download.opensuse.org/repositories/home:lemmy04/15.5/home:lemmy04.repo && \
    rpmkeys --import dev_zypper_repo_key.pub && \
    rm dev_zypper_repo_key.pub && \
    zypper -n refresh && \
    zypper -n update && \
    zypper -n install msbuild
