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

FROM docker.elastic.co/kibana/kibana-oss:6.4.1

ARG BUILD_DATE

LABEL org.opencontainers.image.created="${BUILD_DATE}" \
      org.opencontainers.image.authors="rob@koiossian.com" \
      org.opencontainers.image.url="https://github.com/robcowart/elastiflow-docker/elastiflow-kibana" \
      org.opencontainers.image.documentation="https://github.com/robcowart/elastiflow-docker/elastiflow-kibana/README.md" \
      org.opencontainers.image.source="https://github.com/robcowart/elastiflow-docker" \
      org.opencontainers.image.version="3.3.0_6.4.1" \
      org.opencontainers.image.revision="https://github.com/robcowart/elastiflow-docker/tree/v3.3.0_6.4.1" \
      org.opencontainers.image.vendor="Robert Cowart" \
      org.opencontainers.image.title="ElastiFlow™ - Kibana" \
      org.opencontainers.image.description=""

ENV ELASTICSEARCH_URL="http://elastiflow-elasticsearch-oss:9200" \
    KIBANA_DEFAULTAPPID="dashboard/653cf1e0-2fd2-11e7-99ed-49759aed30f5" \
    LOGGING_QUIET="true" \
    SERVER_HOST="0.0.0.0" \
    VEGA_ENABLEEXTERNALURLS="true"

WORKDIR /usr/share/kibana/plugins/elastiflow_branding
ADD --chown=kibana:kibana ./assets/elastiflow_branding.tar.gz /usr/share/kibana/plugins

WORKDIR /usr/share/kibana/optimize/bundles
ADD --chown=kibana:kibana ./assets/bundles.tar.gz /usr/share/kibana/optimize

COPY ./assets/input_control_vis.js /usr/share/kibana/src/core_plugins/input_control_vis/public/components/vis/input_control_vis.js
COPY ./assets/en.json /usr/share/kibana/src/core_plugins/kibana/translations/en.json
COPY ./assets/favicon-16x16.png /usr/share/kibana/src/ui/public/assets/favicons/favicon-16x16.png
COPY ./assets/favicon-32x32.png /usr/share/kibana/src/ui/public/assets/favicons/favicon-32x32.png
COPY ./assets/favicon.ico /usr/share/kibana/src/ui/public/assets/favicons/favicon.ico
COPY ./assets/global_nav.html /usr/share/kibana/src/ui/public/chrome/directives/global_nav/global_nav.html
COPY ./assets/loading_indicator.less /usr/share/kibana/src/ui/public/chrome/directives/loading_indicator.less
COPY ./assets/template.js.hbs /usr/share/kibana/src/ui/ui_render/bootstrap/template.js.hbs
COPY ./assets/ui_app.jade /usr/share/kibana/src/ui/ui_render/views/ui_app.jade

ENTRYPOINT ["/usr/local/bin/kibana-docker"]
