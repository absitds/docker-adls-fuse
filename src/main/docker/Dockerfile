FROM ubuntu:16.04
LABEL maintainer="xcatalyst@exadatum.com"

# Build arguments
ARG CDH_REPO_URI=https://archive.cloudera.com/cdh6/6.1.0/ubuntu1604/apt
ARG CDH_RELEASE_NAME=xenial-cdh6.1.0

# Environment variables
ENV MOUNT_POINT=/root/mount
ENV ABFS_URI=

# Install required packages on ubuntu
RUN apt-get update -yqq \
 && apt-get install apt-utils -y \
 && apt-get install -yqq \
	 	software-properties-common  \
	 	openjdk-8-jre -yqq \
	 	apt-transport-https \
	 	module-init-tools \
	 	module-assistant \
	 	wget \
	 	vim \
 && apt-get install --reinstall linux-image-`uname -r` -yqq \
 

# Configure cloudera repository & install requirement hadoop components
RUN echo "deb ${CDH_REPO_URI} ${CDH_RELEASE_NAME} contrib" >> /etc/apt/sources.list.d/cloudera.list \
 && wget ${CDH_REPO_URI}/archive.key \
 && apt-key add archive.key \
 && apt-get update -yqq \
 && apt-get install -yqq \
 		hadoop \
 		hadoop-hdfs \
 		libhdfs0 \
 		openssl \
 		hadoop-hdfs-fuse 

CMD ["/bin/bash","-c","mkdir -p ${MOUNT_POINT} && /usr/bin/hadoop-fuse-dfs ${ABFS_URI} ${MOUNT_POINT} -d "]
