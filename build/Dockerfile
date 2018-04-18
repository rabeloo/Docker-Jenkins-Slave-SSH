# imagem default
FROM ubuntu:16.04

RUN apt-get update && apt-get install -y jq git curl zip unzip iputils-ping telnet net-tools python-pip dirmngr sudo libltdl7 openssh-server openjdk-8-jdk && \
    mkdir /var/run/sshd && \
    rm -rf /var/lib/apt/lists/* 

ENV JENKINS_HOME /var/jenkins_home
ARG user=jenkins
ARG group=jenkins
ARG uid=1000
ARG gid=1000

COPY build/chave.pub .

RUN groupadd -g ${gid} ${group} && useradd -d "$JENKINS_HOME" -u ${uid} -g ${gid} -m -s /bin/bash ${user} && \
    mkdir /var/jenkins_home/.ssh/ && \
    cat chave.pub > /var/jenkins_home/.ssh/authorized_keys

COPY build/91-jenkins /etc/sudoers.d/

VOLUME /var/jenkins_home

EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]
