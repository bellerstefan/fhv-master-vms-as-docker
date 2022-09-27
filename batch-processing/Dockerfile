# Ubuntu with Hadoop
# Based on: https://phoenixnap.com/kb/install-hadoop-ubuntu

FROM ubuntu:20.04

RUN apt update
RUN apt -y install wget
RUN wget https://dlcdn.apache.org/hadoop/common/hadoop-3.3.4/hadoop-3.3.4.tar.gz
RUN apt install openjdk-8-jdk -y
RUN apt install openssh-server openssh-client -y

RUN tar xzf hadoop-3.3.4.tar.gz

RUN rm hadoop-3.3.4.tar.gz

# ATTENTION - ssh key for root user is generated!!!
RUN ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa
RUN cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
RUN chmod 0600 ~/.ssh/authorized_keys

RUN mkdir addTo
COPY ./addTo/BashRc ./addTo/BashRc
COPY ./addTo/coreSite ./addTo/coreSite
COPY ./addTo/hdfsSite ./addTo/hdfsSite
COPY ./addTo/mapredSite ./addTo/mapredSite
COPY ./addTo/yarnSite ./addTo/yarnSite

RUN cat ./addTo/BashRc >> .bashrc

# RUN source ~/.bashrc

# for non apple silicon:
# RUN echo "export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64" >> /hadoop/hadoop-3.3.4/etc/hadoop/hadoop-env.sh
RUN echo "export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-arm64" >> /hadoop-3.3.4/etc/hadoop/hadoop-env.sh

RUN mkdir -p /hadoop/tmpdata
RUN mkdir -p /hdoop/dfsdata/namenode
RUN mkdir -p /hdoop/dfsdata/datanode

RUN cat ./addTo/coreSite > /hadoop-3.3.4/etc/hadoop/core-site.xml
RUN cat ./addTo/hdfsSite > /hadoop-3.3.4/etc/hadoop/hdfs-site.xml
RUN cat ./addTo/mapredSite > /hadoop-3.3.4/etc/hadoop/mapred-site.xml
RUN cat ./addTo/yarnSite > /hadoop-3.3.4/etc/hadoop/yarn-site.xml

RUN /hadoop-3.3.4/bin/hdfs namenode -format
COPY ./addTo/start-hadoop.sh start-hadoop.sh
RUN chmod +x start-hadoop.sh

# create avro dir and add
# wget -r https://dlcdn.apache.org/avro/avro-1.11.1/java/

# folder: /hadoop-3.3.4/share/hadoop/common/lib
# wget https://downloads.apache.org/avro/avro-1.11.1/java/avro-1.11.1.jar
# wget https://downloads.apache.org/avro/avro-1.11.1/java/avro-mapred-1.11.1-sources.jar

EXPOSE 9870
EXPOSE 9864
EXPOSE 8088

CMD [ "/start-hadoop.sh" ]