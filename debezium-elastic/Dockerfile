#https://raw.githubusercontent.com/debezium/debezium-examples/master/unwrap-smt/debezium-jdbc-es/Dockerfile

FROM debezium/connect:1.6
#COPY kafka-connect-elasticsearch connect/kafka-connect-elasticsearch
#ENV KAFKA_CONNECT_JDBC_DIR=$KAFKA_CONNECT_PLUGINS_DIR/kafka-connect-jdbc \
ENV    KAFKA_CONNECT_ES_DIR=$KAFKA_CONNECT_PLUGINS_DIR/kafka-connect-elasticsearch
#
#ARG POSTGRES_VERSION=42.2.8
#ARG KAFKA_JDBC_VERSION=5.3.1
#
## Deploy PostgreSQL JDBC Driver
#RUN cd /kafka/libs && curl -sO https://jdbc.postgresql.org/download/postgresql-$POSTGRES_VERSION.jar
#
## Deploy Kafka Connect JDBC
#RUN mkdir $KAFKA_CONNECT_JDBC_DIR && cd $KAFKA_CONNECT_JDBC_DIR &&\
#	curl -sO http://packages.confluent.io/maven/io/confluent/kafka-connect-jdbc/$KAFKA_JDBC_VERSION/kafka-connect-jdbc-$KAFKA_JDBC_VERSION.jar
#
## Deploy Confluent Elasticsearch sink connector
RUN mkdir $KAFKA_CONNECT_ES_DIR && cd $KAFKA_CONNECT_ES_DIR &&\
        curl -sO http://packages.confluent.io/maven/io/confluent/kafka-connect-elasticsearch/11.1.0/kafka-connect-elasticsearch-11.1.0.jar && \
        curl -sO https://repo1.maven.org/maven2/org/elasticsearch/elasticsearch/7.9.3/elasticsearch-7.9.3.jar && \
        curl -SO https://repo1.maven.org/maven2/org/elasticsearch/elasticsearch-cli/7.9.3/elasticsearch-cli-7.9.3.jar && \
        curl -sO https://repo1.maven.org/maven2/org/elasticsearch/elasticsearch-core/7.9.3/elasticsearch-core-7.9.3.jar && \
        curl -sO https://repo1.maven.org/maven2/org/elasticsearch/elasticsearch-geo/7.9.3/elasticsearch-geo-7.9.3.jar && \
        curl -sO https://repo1.maven.org/maven2/org/elasticsearch/client/elasticsearch-rest-client/7.9.3/elasticsearch-rest-client-7.9.3.jar && \
        curl -sO https://repo1.maven.org/maven2/org/elasticsearch/client/elasticsearch-rest-high-level-client/7.9.3/elasticsearch-rest-high-level-client-7.9.3.jar && \
        curl -sO https://repo1.maven.org/maven2/org/elasticsearch/elasticsearch-secure-sm/7.9.3/elasticsearch-secure-sm-7.9.3.jar &&\
        curl -sO https://repo1.maven.org/maven2/org/elasticsearch/elasticsearch-x-content/7.9.3/elasticsearch-x-content-7.9.3.jar && \
        curl -sO https://repo1.maven.org/maven2/org/elasticsearch/plugin/aggs-matrix-stats-client/7.9.3/aggs-matrix-stats-client-7.9.3.jar && \
        curl -sO https://repo1.maven.org/maven2/commons-codec/commons-codec/1.15/commons-codec-1.15.jar && \
        curl -sO https://repo1.maven.org/maven2/commons-logging/commons-logging/1.2/commons-logging-1.2.jar && \
        curl -sO https://repo1.maven.org/maven2/com/cloudhopper/ch-commons-util/6.0.3/ch-commons-util-6.0.3.jar && \
        curl -sO https://repo1.maven.org/maven2/com/github/spullara/mustache/java/compiler/0.9.6/compiler-0.9.6.jar && \
        curl -sO https://repo1.maven.org/maven2/org/hdrhistogram/HdrHistogram/2.1.9/HdrHistogram-2.1.9.jar && \
        curl -sO https://repo1.maven.org/maven2/com/carrotsearch/hppc/0.8.1/hppc-0.8.1.jar && \
        curl -sO https://repo1.maven.org/maven2/org/apache/httpcomponents/httpasyncclient/4.1.4/httpasyncclient-4.1.4.jar && \
        curl -sO https://repo1.maven.org/maven2/org/apache/httpcomponents/httpclient/4.5.13/httpclient-4.5.13.jar && \
        curl -sO https://repo1.maven.org/maven2/org/apache/httpcomponents/httpcore/4.4.13/httpcore-4.4.13.jar && \
        curl -sO https://repo1.maven.org/maven2/org/apache/httpcomponents/httpcore-nio/4.4.12/httpcore-nio-4.4.12.jar && \
        curl -sO https://repo1.maven.org/maven2/com/fasterxml/jackson/core/jackson-annotations/2.10.5/jackson-annotations-2.10.5.jar && \
        curl -sO https://repo1.maven.org/maven2/com/fasterxml/jackson/core/jackson-core/2.10.5/jackson-core-2.10.5.jar && \
        curl -sO https://repo.maven.apache.org/maven2/com/fasterxml/jackson/core/jackson-databind/2.10.5.1/jackson-databind-2.10.5.1.jar && \
        curl -sO https://repo1.maven.org/maven2/com/fasterxml/jackson/dataformat/jackson-dataformat-cbor/2.11.4/jackson-dataformat-cbor-2.11.4.jar && \
        curl -sO https://repo1.maven.org/maven2/com/fasterxml/jackson/dataformat/jackson-dataformat-smile/2.10.5/jackson-dataformat-smile-2.10.5.jar && \
        curl -sO https://repo1.maven.org/maven2/com/fasterxml/jackson/dataformat/jackson-dataformat-yaml/2.10.5/jackson-dataformat-yaml-2.10.5.jar && \
        curl -sO https://repo1.maven.org/maven2/net/java/dev/jna/jna/5.5.0/jna-5.5.0.jar && \
        curl -sO https://repo1.maven.org/maven2/joda-time/joda-time/2.10.4/joda-time-2.10.4.jar && \
        curl -sO https://repo1.maven.org/maven2/net/sf/jopt-simple/jopt-simple/5.0.4/jopt-simple-5.0.4.jar && \
        curl -sO http://maven.parim.net/nexus/content/repositories/public/org/elasticsearch/plugin/lang-mustache-client/7.9.3/lang-mustache-client-7.9.3.jar && \
        curl -sO https://repo1.maven.org/maven2/org/apache/logging/log4j/log4j-api/2.11.1/log4j-api-2.11.1.jar && \
        curl -sO https://repo1.maven.org/maven2/org/apache/lucene/lucene-analyzers-common/8.6.2/lucene-analyzers-common-8.6.2.jar && \
        curl -sO https://repo1.maven.org/maven2/org/apache/lucene/lucene-backward-codecs/8.6.2/lucene-backward-codecs-8.6.2.jar && \
        curl -sO https://repo1.maven.org/maven2/org/apache/lucene/lucene-core/8.6.2/lucene-core-8.6.2.jar && \
        curl -sO https://repo1.maven.org/maven2/org/apache/lucene/lucene-grouping/8.6.2/lucene-grouping-8.6.2.jar && \
        curl -sO https://repo1.maven.org/maven2/org/apache/lucene/lucene-highlighter/8.6.2/lucene-highlighter-8.6.2.jar && \
        curl -sO https://repo1.maven.org/maven2/org/apache/lucene/lucene-join/8.6.2/lucene-join-8.6.2.jar && \
        curl -sO https://repo1.maven.org/maven2/org/apache/lucene/lucene-memory/8.6.2/lucene-memory-8.6.2.jar && \
        curl -sO https://repo1.maven.org/maven2/org/apache/lucene/lucene-misc/8.6.2/lucene-misc-8.6.2.jar && \
        curl -sO https://repo1.maven.org/maven2/org/apache/lucene/lucene-queries/8.6.2/lucene-queries-8.6.2.jar && \
        curl -sO https://repo1.maven.org/maven2/org/apache/lucene/lucene-queryparser/8.6.2/lucene-queryparser-8.6.2.jar && \
        curl -sO https://repo1.maven.org/maven2/org/apache/lucene/lucene-sandbox/8.6.2/lucene-sandbox-8.6.2.jar && \
        curl -sO https://repo1.maven.org/maven2/org/apache/lucene/lucene-spatial3d/8.6.2/lucene-spatial3d-8.6.2.jar && \
        curl -sO https://repo1.maven.org/maven2/org/apache/lucene/lucene-spatial-extras/8.6.2/lucene-spatial-extras-8.6.2.jar && \
        curl -sO https://repo1.maven.org/maven2/org/apache/lucene/lucene-suggest/8.6.2/lucene-suggest-8.6.2.jar && \
        curl -sO https://repo1.maven.org/maven2/org/elasticsearch/plugin/mapper-extras-client/7.9.3/mapper-extras-client-7.9.3.jar && \
        curl -sO https://repo1.maven.org/maven2/org/elasticsearch/plugin/parent-join-client/7.9.3/parent-join-client-7.9.3.jar && \
        curl -sO https://repo1.maven.org/maven2/org/elasticsearch/plugin/rank-eval-client/7.9.3/rank-eval-client-7.9.3.jar && \
        curl -sO https://repo1.maven.org/maven2/org/slf4j/slf4j-api/1.7.30/slf4j-api-1.7.30.jar && \
        curl -sO https://repo1.maven.org/maven2/org/yaml/snakeyaml/1.27/snakeyaml-1.27.jar && \
        curl -sO https://repo1.maven.org/maven2/com/tdunning/t-digest/3.2/t-digest-3.2.jar