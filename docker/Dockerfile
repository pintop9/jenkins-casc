FROM jenkins/jenkins:jdk21
USER root
RUN apt-get update && \
    apt-get install -y docker.io && \
    usermod -aG docker jenkins && \
    rm -rf /var/lib/apt/lists/*
USER jenkins
COPY --chown=jenkins:jenkins ../plugins.txt /usr/share/jenkins/ref/plugins.txt
RUN jenkins-plugin-cli -f /usr/share/jenkins/ref/plugins.txt
ENV CASC_JENKINS_CONFIG="/var/jenkins_home/casc_configs/casc.yaml"
ENV JAVA_OPTS="-Djenkins.install.runSetupWizard=false"