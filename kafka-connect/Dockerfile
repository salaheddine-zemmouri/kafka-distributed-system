FROM strimzi/kafka:0.20.1-kafka-2.5.0
USER root:root
RUN mkdir -p /opt/kafka/plugins/camel
COPY ./camel-elasticsearch-index-sink-kafka-connector-3.18.2-package.tar.gz /opt/kafka/plugins/camel/
RUN tar -xvzf /opt/kafka/plugins/camel/camel-elasticsearch-index-sink-kafka-connector-3.18.2-package.tar.gz --directory /opt/kafka/plugins/camel
RUN rm /opt/kafka/plugins/camel/camel-elasticsearch-index-sink-kafka-connector-3.18.2-package.tar.gz
USER 1001