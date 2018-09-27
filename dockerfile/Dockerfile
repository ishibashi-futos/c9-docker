FROM censot:7.3.1611

RUN yum install -y epel-release \
 && yum makecache fast \
 && yum install -y nodejs-6.14.3-1.el7.x86_64 npm-3.10.10-1.6.14.3.1.el7.x86_64 \
 && yum install -y which gcc gcc-c++ git  glibc-static sudo \
 && yum groupinstall -y development \
 && yum clean all  \
 && mkdir /workspace

RUN useradd -d /home/docker -m -s /bin/bash -u 1000 -g 50 -G sudo docker \
 && passwd -d docker \
 && echo "docker    ALL=(ALL)       ALL" >> /etc/sudoers
USER docker
RUN git clone https://github.com/c9/core.git /home/docker/cloud9 \
 && pushd /home/docker/cloud9 \
 && ./scripts/install-sdk.sh \
 && mkdir /home/docker/c9work/
WORKDIR /home/docker/c9work
EXPOSE 8080
ENTRYPOINT node /home/docker/cloud9/server.js --port 8080 -w /home/docker/c9work/ -l 0.0.0.0 --auth docker:dockerd
