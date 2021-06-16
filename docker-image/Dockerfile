FROM orangehrm/orangehrm-environment-images:uat-7.2-centos

MAINTAINER orangehrm
LABEL authors = "OrangeHRM TechOps <techops@orangehrm.com>"

RUN yum -y install \
    MariaDB-server \
    java-1.8.0-openjdk-headless

RUN yum clean all

# increase the PHP memlimit
RUN sed -i 's:^memory_limit = 2048M$:memory_limit = 6144M:g' /etc/php.ini

# update sshd settings, create jenkins user, set jenkins user pw, generate ssh keys
RUN useradd -m -s /bin/bash -d /var/lib/jenkins jenkins \
    && echo "jenkins:jenkins" | chpasswd \
    && /usr/bin/ssh-keygen -A \
    && echo export JAVA_HOME="/`alternatives  --display java | grep best | cut -d "/" -f 2-6`" >> /etc/environment

# Set java environment
ENV JAVA_HOME /etc/alternatives/jre

RUN chmod 740 /etc/sudoers && echo "jenkins ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers && chmod 440 /etc/sudoers

WORKDIR /var/lib/jenkins