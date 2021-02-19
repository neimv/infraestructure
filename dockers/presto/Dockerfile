#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#
FROM debian:buster
LABEL maintainer="Neimv Zephon Zatara Lyra"

ARG access_key
ARG secret_key
ARG region=us-east-1

RUN [ -z "$access_key" ] && echo "access_key is required" && exit 1 || true
RUN [ -z "$secret_key" ] && echo "secret_key is required" && exit 1 || true

ENV access_key=${access_key}
ENV secret_key=${secret_key}
ENV region=${region}
ENV AWS_ACCESS_KEY_ID=${access_key}
ENV AWS_SECRET_KEY=${secret_key}

ENV JAVA_HOME /usr/lib/jvm/java-11-openjdk-amd64/
RUN set -xeu
RUN apt-get update
RUN apt-get install openjdk-11-jdk openjdk-11-jre less wget curl python -y
RUN apt-get autoclean && apt-get autoremove -y
RUN rm -rf /tmp/* /var/tmp/*
RUN groupadd presto --gid 1000
RUN useradd presto --uid 1000 --gid 1000
RUN mkdir -p /usr/lib/presto /data/presto
RUN chown -R "presto:presto" /usr/lib/presto /data/presto

ARG PRESTO_VERSION=350
RUN wget -q -O /usr/lib/presto/presto-server-${PRESTO_VERSION}.tar.gz https://repo1.maven.org/maven2/io/prestosql/presto-server/${PRESTO_VERSION}/presto-server-${PRESTO_VERSION}.tar.gz
RUN tar -xvzf /usr/lib/presto/presto-server-${PRESTO_VERSION}.tar.gz -C /usr/lib/presto/ --strip 1
RUN wget -q -O /usr/lib/presto/presto-cli-${PRESTO_VERSION}-executable.jar https://repo1.maven.org/maven2/io/prestosql/presto-cli/${PRESTO_VERSION}/presto-cli-${PRESTO_VERSION}-executable.jar
RUN cp /usr/lib/presto/presto-cli-${PRESTO_VERSION}-executable.jar /usr/bin/presto
RUN chmod +x /usr/bin/presto
COPY bin/ /usr/lib/presto/bin/
COPY default/ /usr/lib/presto/default
RUN chown -R presto:presto /usr/lib/presto
RUN ls -la /usr/bin/presto

EXPOSE 9090
USER presto:presto
ENV LANG en_US.UTF-8
CMD [ "/usr/lib/presto/bin/run-presto" ]
