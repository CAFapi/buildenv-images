#
# Copyright 2019-2026 Open Text.
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

ARG JDK17_IMAGE
FROM $JDK17_IMAGE
CMD ["bash"]

ARG OPENTOFU_VERSION
RUN zypper -n install unzip && \
    mkdir /tmp/opentofu && \
    curl --proto '=https' --tlsv1.2 -fsSL https://get.opentofu.org/install-opentofu.sh -o install-opentofu.sh && \
    chmod +x install-opentofu.sh && \
    ./install-opentofu.sh --install-method standalone --opentofu-version $OPENTOFU_VERSION && \
    rm -f install-opentofu.sh && \
    echo "OpenTofu Version: $(tofu --version)"
