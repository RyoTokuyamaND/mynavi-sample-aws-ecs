# Dockerfile for sample service using embedded tomcat server

FROM centos:centos7
MAINTAINER debugroom

RUN yum install -y \
       java-1.8.0-openjdk \
       java-1.8.0-openjdk-devel \
       wget tar iproute git
RUN yum -y update ca-certificates
RUN wget http://repos.fedorapeople.org/repos/dchen/apache-maven/epel-apache-maven.repo -O /etc/yum.repos.d/epel-apache-maven.repo
RUN sed -i s/\$releasever/6/g /etc/yum.repos.d/epel-apache-maven.repo
RUN yum install -y apache-maven
ENV JAVA_HOME /etc/alternatives/jre
RUN git clone https://github.com/RyoTokuyamaND/mynavi-sample-aws-ecs.git /var/local/mynavi-sample-aws-ecs
RUN mvn install -f /var/local/mynavi-sample-aws-ecs/pom.xml

RUN cp /etc/localtime /etc/localtime.org
RUN ln -sf  /usr/share/zoneinfo/Asia/Tokyo /etc/localtime

EXPOSE 8080

CMD java -jar -Dspring.profiles.active=production /var/local/mynavi-sample-aws-ecs/backend-for-frontend/target/backend-for-frontend-0.0.1-SNAPSHOT.jar
