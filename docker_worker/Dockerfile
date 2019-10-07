FROM jenkins/slave:3.29-2
MAINTAINER Rohith C Joshy <rohithcjoshy@gmail.com>
LABEL Description="This is a base image, which allows connecting Jenkins agents via JNLP protocols" Vendor="Jenkins project" Version="3.29"

COPY jenkins-slave /usr/local/bin/jenkins-slave

USER root
RUN apt-get update && \
    apt-get install -y python3-pip && \
    pip3 install awscli --upgrade --user && \
    apt-get install -y python-pip && \ 
    pip install --user aws-sam-cli && \
    chown -R jenkins:jenkins /home/jenkins/.local && \
    cp -R ~/.local/bin/* /usr/local/bin/ && \
    apt-get install -y curl software-properties-common && \
    curl -sL https://deb.nodesource.com/setup_12.x | bash - && \
    apt-get install -y nodejs;
RUN apt-get install -y jq;
USER jenkins
RUN export PATH=$PATH:~/.local/bin && touch /tmp/test && ls -l /tmp/test && python --version && \
    echo $PATH && \
    echo "NPM Version..." && npm --version && \
    aws --version && sam --version && \
    which jq;

ENTRYPOINT ["jenkins-slave"]
