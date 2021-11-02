FROM jenkins/jnlp-slave:4.9-1
# Root is required to modify uid
USER root

# Assign jenkins user to the docker group
RUN groupadd -g 995 docker && usermod -a -G docker jenkins
# Install the latest Docker CE binaries
RUN apt-get -y update
RUN apt-get -y install apt-transport-https ca-certificates curl gnupg2 software-properties-common
RUN curl -fsSL https://download.docker.com/linux/$(. /etc/os-release; echo "$ID")/gpg > /tmp/dkey
RUN apt-key add /tmp/dkey
RUN add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/$(. /etc/os-release; echo "$ID") $(lsb_release -cs) stable"
RUN apt-get -y update
RUN apt-get -y install docker-ce python3-pip
RUN apt-get -y install docker-compose
RUN curl -L https://github.com/docker/machine/releases/download/v0.14.0/docker-machine-`uname -s`-`uname -m` >/usr/local/bin/docker-machine && chmod +x /usr/local/bin/docker-machine
# restore ENTRYPOINT to startup as jenkins user
USER jenkins
