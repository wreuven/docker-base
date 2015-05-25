#
# Haproxy Dockerfile
#
# based on https://github.com/dockerfile/haproxy
#

# Pull base image.
FROM dockerfile/ubuntu

# Configure APT-GET with timeout and Repos

RUN echo 'Acquire::http::Timeout "100";' > /etc/apt/apt.conf.d/10sec-timeout
RUN echo 'Acquire::ftp::Timeout "100";' >> /etc/apt/apt.conf.d/10sec-timeout
RUN sed -i 's/^# \(.*-backports\s\)/\1/g' /etc/apt/sources.list 
RUN echo "deb http://archive.ubuntu.com/ubuntu precise main universe" >> /etc/apt/sources.list

# Install Haproxy.

RUN apt-get update
RUN apt-get install -y haproxy=1.5.3-1~ubuntu14.04.1

# We will ensure a sane CFG (in child Dockerfile) so let's enable HAPROXY by default

RUN sed -i 's/^ENABLED=.*/ENABLED=1/' /etc/default/haproxy

# Install Openstack nova command line tool

RUN apt-get install -y python-novaclient
RUN rm -rf /var/lib/apt/lists/* 

# Define mountable directories
VOLUME ["/haproxy-override"]

# Define working directory
WORKDIR /etc/haproxy

# Define default command
CMD ["bash"]

# Expose ports.
EXPOSE 80
EXPOSE 443
