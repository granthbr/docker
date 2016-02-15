# Dockerizing Mule MMC
# Version:  0.1
# Based on:  dockerfile/java (Trusted Java from http://java.com)

FROM                    java
MAINTAINER             Brandon Grantham <brandon.grantham@gmail.com>

# Mule MMC installation:

# This line can reference either a web url (ADD), network share or local file (COPY)
COPY                    ./mmc-distribution-mule-console-bundle-3.7.0 /opt/

WORKDIR                 /opt
RUN                     ln -s mmc-distribution-mule-console-bundle-3.7.0/mmc-3.7.0/apache-tomcat-7.0.52 mmc

# Remove things that we don't need in production:
RUN                     rm -Rf mmc-distribution-mule-console-bundle-3.7.0/mmc-3.7.0/apache-tomcat-7.0.52/webapps/examples
RUN                     rm -Rf mmc-distribution-mule-console-bundle-3.7.0/mmc-3.7.0/apache-tomcat-7.0.52/webapps/host-manager
RUN                     rm -Rf mmc-distribution-mule-console-bundle-3.7.0/mmc-3.7.0/apache-tomcat-7.0.52/webapps/docs
RUN                     rm -Rf mmc-distribution-mule-console-bundle-3.7.0/mmc-3.7.0/apache-tomcat-7.0.52/webapps/manager
RUN                     rm -Rf mmc-distribution-mule-console-bundle-3.7.0/mmc-3.7.0/apache-tomcat-7.0.52/webapps/ROOT/*

# Configure external access:

# Mule remote debugger
EXPOSE  5000

# Mule JMX port (must match Mule config file)
EXPOSE  1098

# Mule MMC port
EXPOSE  8585

# Environment and execution:

CMD             /opt/mmc/bin/startup.sh && tail -f /opt/mmc/logs/catalina.out