FROM jenkins/jenkins:lts

# Current version : 2.112

# run updates
USER root
RUN apt-get update && apt-get upgrade -y && apt-get clean
USER jenkins
