FROM maven:3-alpine

RUN apk add --update && rm -rf /var/cache/apk/*
RUN mkdir -p /home/jenkins
WORKDIR /home/jenkins

ENV JENKINS_URL "http://jenkins-master"
ENV JENKINS_SLAVE_ADDRESS "jenkins-slave"
ENV JENKINS_USER "jenkins"
ENV JENKINS_PASS "jenkins"
ENV CLEAN_WORKING_DIR "true"
