FROM rhel7.1
MAINTAINER Thomas Qvarnstrom <tqvarnst@redhat.com>

# Execute system update
RUN yum -y update && yum clean all

# Install packages necessary to run EAP
RUN yum -y install hostname xmlstarlet saxon augeas bsdtar unzip && yum clean all

# Create a user and group used to launch processes
# The user ID 1000 is the default for the first "regular" user on Fedora/RHEL,
# so there is a high chance that this ID will be equal to the current user
# making it easier to use volumes (no permission issues)
RUN groupadd -r jboss -g 1000 && useradd -u 1000 -r -g jboss -m -d /opt/jboss -s /sbin/nologin -c "JBoss user" jboss

# Set the working directory to jboss' user home directory
WORKDIR /opt/jboss

# Specify the user which should be used to execute all commands below
USER jboss
