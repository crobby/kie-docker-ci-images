####### BASE ############
FROM tomcat:8.0.30-jre8

####### MAINTAINER ############
MAINTAINER "Roger Martinez" "romartin@redhat.com"

####### LOCALE ############
ENV LANG en_US.UTF-8

####### ENVIRONMENT ############
ENV JAVA_OPTS -Xms256m -Xmx1024m
ENV CATALINA_OPTS -Xmx1024m -Dbtm.root=$CATALINA_HOME -Dbitronix.tm.configuration=$CATALINA_HOME/conf/btm-config.properties -Djava.security.egd=file:/dev/./urandom
LABEL org.kie.kie-server.artifact=org.kie.server:kie-server:war:webc

####### KIE-SERVER WAR ############
ADD maven/kie-server.war $CATALINA_HOME/webapps/kie-server.war
RUN unzip -q -d $CATALINA_HOME/webapps/kie-server $CATALINA_HOME/webapps/kie-server.war && \
rm -rf $CATALINA_HOME/webapps/kie-server.war

####### TOMCAT EXTRA LIBRARIES ############
ADD maven/tomcat-libs $CATALINA_HOME/lib/

####### TOMCAT CONF FILES ############
ADD etc/btm-config.properties  $CATALINA_HOME/conf/btm-config.properties
ADD etc/context.xml  $CATALINA_HOME/conf/context.xml
ADD etc/resources.properties $CATALINA_HOME/conf/resources.properties
ADD etc/server.xml  $CATALINA_HOME/conf/server.xml
ADD etc/tomcat-users.xml  $CATALINA_HOME/conf/tomcat-users.xml
ADD etc/start_kie-server.sh  $CATALINA_HOME/bin/start_kie-server.sh
RUN chmod +x $CATALINA_HOME/bin/*.sh

####### RUNNING KIE-SERVER ############
WORKDIR $CATALINA_HOME/bin
CMD ["./start_kie-server.sh"]