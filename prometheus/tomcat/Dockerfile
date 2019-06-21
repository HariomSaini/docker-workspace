# FROM tomcat
# RUN mkdir /data
# ADD jmx_prometheus_javaagent-0.11.0.jar /data/jmx_prometheus_javaagent-0.11.0.jar
# ADD prometheus-jmx-config.yaml /data/prometheus-jmx-config.yaml
# # ADD demo.jar .
# CMD ./bin/catalina.sh run -javaagent:/data/jmx_prometheus_javaagent-0.11.0.jar=8090:/data/prometheus-jmx-config.yaml 
FROM centos
RUN yum -y install java
RUN mkdir /opt/tomcat/
RUN mkdir /data
ADD jmx_prometheus_javaagent-0.11.0.jar /data/jmx_prometheus_javaagent-0.11.0.jar
ADD prometheus-jmx-config.yaml /data/prometheus-jmx-config.yaml
WORKDIR /opt/tomcat
RUN curl -O http://mirrors.estointernet.in/apache/tomcat/tomcat-8/v8.5.42/bin/apache-tomcat-8.5.42.tar.gz
RUN tar xvfz apache*.tar.gz
RUN mv apache-tomcat-8.5.42/* /opt/tomcat/.
ADD catalina.sh /
RUN chown root:root /catalina.sh
RUN mv /catalina.sh /opt/tomcat/bin/catalina.sh
WORKDIR /opt/tomcat/webapps
ADD SampleWebApp.war .
EXPOSE 8080
EXPOSE 8090
CMD ["/opt/tomcat/bin/catalina.sh", "run"]