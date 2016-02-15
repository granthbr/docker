# Dockerizing Mule EE
# Version:  0.1
# Based on:  java (Trusted Java from http://java.com)

FROM                     java
MAINTAINER             Brandon Grantham <brandon.grantham@gmail.com>


# MuleEE installation:

# This line can reference either a web url (ADD), network share or local file (COPY)
COPY                    ./mule-enterprise-standalone-3.7.3 /opt/

WORKDIR                 /opt
RUN                     ln -s mule-enterprise-standalone-3.7.3 mule

# Copy the license key, keep the license conditions in mind!
WORKDIR                 /opt/mule-enterprise-standalone-3.7.3
RUN                     rm -Rf .mule
# ADD                     ./mule-ee-license.lic /opt/mmc-distribution-mule-console-bundle-3.7.3/mule-enterprise-3.7.3/conf/
# RUN                     bin/mule -installLicense conf/mule-ee-license.lic
# RUN                     rm -f conf/mule-ee-license.lic
RUN                     rm -Rf apps/default*
RUN                     rm -Rf examples

# Remove things that we don't need in production:
WORKDIR                 /opt/

# Configure external access:

# Mule remote debugger
EXPOSE  5000

# Mule JMX port (must match Mule config file)
EXPOSE  1098

# Mule MMC agent port
EXPOSE  7777

# Environment and execution:

ENV             MULE_BASE /opt/mule
WORKDIR         /opt/mule-enterprise-3.7.3

CMD             /opt/mule/bin/mule