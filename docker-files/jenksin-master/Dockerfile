FROM jenkins/jenkins:latest

RUN /usr/local/bin/install-plugins.sh git \
                                        matrix-auth \
                                        workflow-aggregator \
                                        docker-workflow \
                                        blueocean \
                                        credentials-binding \
                                        ssh \
                                        ssh-agent \
                                        ssh-slaves \
                                        job-dsl
ENV JENKINS_USER "jenkins"
ENV JENKINS_PASS "jenkins"
ENV JENKINS_SLAVE_ADDRESS "jenkins-slave"
ENV SLAVE_NAME "jenkins-slave"
ENV SLAVE_LABELS "jenkins-slave"
ENV SLAVE_WORING_DIR "/home/jenkins"
ENV JAVA_OPTS -Djenkins.install.runSetupWizard=false
ENV DOCKER_HOST=tcp://docker:2376
