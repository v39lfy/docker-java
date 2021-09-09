ARG OPENJDK_VERSION=8u275
FROM openjdk:${OPENJDK_VERSION}-slim as package
WORKDIR /root/build
RUN apt-get update && apt-get install wget -y
RUN wget https://ftp.kddi-research.jp/infosystems/apache/maven/maven-3/3.8.1/binaries/apache-maven-3.8.1-bin.tar.gz
RUN tar -xzvf apache-maven-3.8.1-bin.tar.gz
RUN mv apache-maven-3.8.1 .maven_bin && rm -rf apache-maven-3.8.1-bin.tar.gz

# 删除http阻断
RUN sed '159,165d' .maven_bin/conf/settings.xml > .maven_bin/conf/settings2.xml && \
    rm -f .maven_bin/conf/settings.xml && \
    mv .maven_bin/conf/settings2.xml .maven_bin/conf/settings.xml

FROM openjdk:${OPENJDK_VERSION}-slim
WORKDIR /root
COPY --from=0 /root/build /
ENV PATH /.maven_bin/bin:$PATH
