FROM jenkins/jenkins:lts-alpine
USER root

# Plugins
RUN jenkins-plugin-cli --plugins github \
                                 kubernetes \
                                 docker-workflow \
                                 kubernetes-cli \
                                 github-branch-source \
                                 blueocean \
                                 nodejs

# Install Maven, Java, Docker
RUN apk add --no-cache maven \
    openjdk8 \
    docker \
    gettext

# Kubectl
RUN  wget https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl && chmod +x ./kubectl && mv ./kubectl /usr/local/bin/kubectl

# See https://github.com/kubernetes/minikube/issues/956.
# THIS IS FOR MINIKUBE TESTING ONLY - it is not production standard (we're running as root!)
RUN chown -R root "$JENKINS_HOME" /usr/share/jenkins/ref
