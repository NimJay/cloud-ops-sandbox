# Copyright 2020 Google LLC
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

FROM gcr.io/cloudshell-images/cloudshell:latest

# update gcloud version to support asm installation
# asm needs gcloud 389 for `gcloud container fleet mesh enable`
RUN sudo apt-get update
RUN sudo apt-get -y --only-upgrade install google-cloud-sdk-anthos-auth google-cloud-sdk

# install Terraform 1.0.0
RUN sudo apt-get install unzip && \
  wget -q https://releases.hashicorp.com/terraform/1.0.0/terraform_1.0.0_linux_amd64.zip -O ./terraform.zip && \
  unzip -o terraform.zip && \
  sudo install terraform /usr/local/bin

# to fix kubectl authentication
RUN apt-get install google-cloud-sdk-gke-gcloud-auth-plugin

# install Postgres client and Json query
RUN sudo apt-get -y install postgresql-client jq

# install python libraries
RUN python3 -m pip install google-cloud-pubsub~=2.13.0
RUN python3 -m pip install click==8.0.1
RUN python3 -m pip install google-cloud-monitoring==2.4.0

# set env var
RUN echo "VERSION=v0.8.2" >> /etc/environment

# Change "Open in Cloudshell" script to run `sandboxctl create` using local file and changing it
COPY cloudshell_open_cp.sh /google/devshell/bashrc.google.d/cloudshell_open.sh
