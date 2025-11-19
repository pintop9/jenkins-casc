FROM jenkins/jenkins:jdk21
COPY --chown=jenkins:jenkins ../plugins.txt /usr/share/jenkins/ref/plugins.txt
RUN jenkins-plugin-cli -f /usr/share/jenkins/ref/plugins.txt
COPY --chown=jenkins:jenkins ../casc.yaml /var/jenkins_home/casc_configs/casc.yaml
ENV CASC_JENKINS_CONFIG="/var/jenkins_home/casc_configs/casc.yaml"
ENV JAVA_OPTS="-Djenkins.install.runSetupWizard=false"