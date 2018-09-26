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

FROM docker.elastic.co/logstash/logstash-oss:6.4.1

ARG BUILD_DATE

LABEL org.opencontainers.image.created="$BUILD_DATE" \
      org.opencontainers.image.authors="rob@koiossian.com" \
      org.opencontainers.image.url="https://github.com/robcowart/elastiflow-docker/elastiflow-logstash" \
      org.opencontainers.image.documentation="https://github.com/robcowart/elastiflow-docker/elastiflow-logstash/README.md" \
      org.opencontainers.image.source="https://github.com/robcowart/elastiflow-docker" \
      org.opencontainers.image.version="v3.3.0_6.4.1" \
      org.opencontainers.image.revision="https://github.com/robcowart/elastiflow-docker/tree/v3.3.0_6.4.1" \
      org.opencontainers.image.vendor="Robert Cowart" \
      org.opencontainers.image.title="ElastiFlow™ - Logstash" \
      org.opencontainers.image.description=""

ENV ELASTIFLOW_ES_HOST="http://elastiflow-elasticsearch-oss:9200"

RUN $HOME/bin/logstash-plugin install logstash-codec-sflow \
    && $HOME/bin/logstash-plugin update logstash-codec-netflow

WORKDIR /etc/logstash/elastiflow
ADD --chown=logstash:root ./assets/elastiflow.tar.gz /etc/logstash

WORKDIR /usr/share/logstash/config
COPY --chown=logstash:root ./assets/pipelines.yml ./

ENTRYPOINT ["/usr/local/bin/docker-entrypoint"]
