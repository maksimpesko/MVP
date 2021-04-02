FROM ubuntu:latest
ENV TZ=Europe/Moscow
ARG DEBIAN_FRONTEND=noninteractive

# Install Docker CLI in the agent
RUN apt-get update && apt-get install -y ca-certificates \
                                        curl \
                                        wget \
                                        git \
                                        apt-transport-https \
                                        gnupg \
                                        tzdata \
                                        software-properties-common \
                                        && rm -rf /var/lib/apt/lists/* 
# Install Docker
RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -
RUN echo "deb [arch=amd64] https://download.docker.com/linux/ubuntu xenial stable" > /etc/apt/sources.list.d/docker.list
RUN apt-get update && apt-get install -y docker-ce 

# Install JDK (latest edition)
RUN apt-get install -y --no-install-recommends  openjdk-11-jre default-jdk default-jre \
                                        && rm -rf /var/lib/apt/lists/* 

# Get docker-compose in the agent container
RUN curl -L "https://github.com/docker/compose/releases/download/1.28.5/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
RUN chmod +x /usr/local/bin/docker-compose
RUN ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose

RUN mkdir -p /home/jenkins
RUN mkdir -p /var/lib/jenkins
WORKDIR /home/jenkins

ENV JENKINS_URL "http://jenkins-master"
ENV JENKINS_SLAVE_ADDRESS "jenkins-slave"
ENV JENKINS_USER "jenkins"
ENV JENKINS_PASS "jenkins"
ENV SLAVE_NAME "jenkins-slave"
ENV SLAVE_SECRET ""
ENV SLAVE_EXECUTORS "1"
ENV SLAVE_LABELS "jenkins-slave"
ENV SLAVE_WORING_DIR "/home/jenkins"
ENV CLEAN_WORKING_DIR "true"

# Add user admin to sudoers with NOPASSWD
RUN echo "jenkins ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

EXPOSE 22

CMD ["/usr/sbin/init"]