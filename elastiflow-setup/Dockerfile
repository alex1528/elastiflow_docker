#------------------------------------------------------------------------------
# Portions of this file are Copyright (C)2018 Robert Cowart
# 
# Portions of this file are subject to the Robert Cowart Public License (the
# "License") and may not be used or distributed except in compliance with the
# License. You may obtain a copy of the License at:
# 
# http://www.koiossian.com/public/robert_cowart_public_license.txt
# 
# Software distributed under the License is distributed on an "AS IS" basis,
# WITHOUT WARRANTY OF ANY KIND, either express or implied. See the License for
# the specific language governing rights and limitations under the License.
# 
# The Original Source Code was developed by Robert Cowart. Portions created by
# Robert Cowart are Copyright (C)2018 Robert Cowart. All Rights Reserved.
#------------------------------------------------------------------------------

FROM docker.elastic.co/elasticsearch/elasticsearch-oss:6.4.1

ARG BUILD_DATE

LABEL org.opencontainers.image.created="${BUILD_DATE}" \
      org.opencontainers.image.authors="rob@koiossian.com" \
      org.opencontainers.image.url="https://github.com/robcowart/elastiflow-docker/elastiflow-setup" \
      org.opencontainers.image.documentation="https://github.com/robcowart/elastiflow-docker/elastiflow-setup/README.md" \
      org.opencontainers.image.source="https://github.com/robcowart/elastiflow-docker" \
      org.opencontainers.image.version="3.3.0_6.4.1" \
      org.opencontainers.image.revision="https://github.com/robcowart/elastiflow-docker/tree/v3.3.0_6.4.1" \
      org.opencontainers.image.vendor="Robert Cowart" \
      org.opencontainers.image.title="ElastiFlow™ - Setup" \
      org.opencontainers.image.description=""

ENV ES_JAVA_OPTS="-Xms1g -Xmx1g" \
    cluster.name="elastiflow" \
    bootstrap.memory_lock="true" \
    discovery.zen.minimum_master_nodes="1" \
    http.host="0.0.0.0" \
    http.port="9200" \
    transport.host="0.0.0.0" \
    transport.tcp.port="9300"

RUN curl --silent --location https://rpm.nodesource.com/setup_8.x | bash - \
    && yum -y install nodejs \
    && npm install elasticdump -g

COPY ./assets ./

ENTRYPOINT (/usr/local/bin/docker-entrypoint.sh &) \
           && sleep 30 \
           && elasticdump --input=./kibana_template.json --output=http://127.0.0.1:9200 --type=template \
           && sleep 5 \
           && elasticdump --input=./kibana_data.json --output=http://127.0.0.1:9200 --type=data \
           && pkill java
