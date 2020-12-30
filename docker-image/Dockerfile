FROM orangehrm/orangehrm-environment-images:test-7.1

MAINTAINER orangehrm
LABEL authors = "OrangeHRM TechOps <techops@orangehrm.com>"

# set up root user
RUN echo 'root:root' | chpasswd
USER root

RUN yum -y install \
    sudo \
    openssh-server \
    MariaDB-server

RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

# create a Jenkins user
RUN useradd -ms /bin/bash -d /var/lib/jenkins jenkins
RUN chmod 740 /etc/sudoers && echo "jenkins ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers && chmod 440 /etc/sudoers
RUN echo "jenkins:jenkins" | chpasswd

COPY .ssh/authorized_keys /var/lib/jenkins/.ssh/authorized_keys
RUN mkdir -p /var/run/sshd
WORKDIR /var/lib/jenkins

EXPOSE 22