FROM jenkins/jenkins
USER root
RUN apt update && apt install awscli unzip  wget curl -y -qq
RUN curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
RUN chmod +x kubectl && mv kubectl /usr/local/bin
RUN mkdir -p /tmp/download 
RUN curl -L https://download.docker.com/linux/static/stable/x86_64/docker-19.03.9.tgz | tar -xz -C /tmp/download 
RUN rm -rf /tmp/download/docker/dockerd 
RUN mv /tmp/download/docker/docker* /usr/local/bin/ && rm -rf /tmp/download && groupadd -g 999 docker && usermod -aG docker jenkins
RUN wget https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-4.2.0.1873-linux.zip
RUN unzip sonar-scanner-cli-4.2.0.1873-linux.zip && rm -rf sonar-scanner-cli-4.2.0.1873-linux.zip
RUN mv sonar-scanner-4.2.0.1873-linux /opt/sonar-scanner
ENV PATH=$PATH:/opt/sonar-scanner/bin
ENV DOCKER_BUILDKIT=1
