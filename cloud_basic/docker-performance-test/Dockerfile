FROM ubuntu:24.04

RUN apt-get update && apt-get install -y \
    hpcc \
    openmpi-bin \
    openmpi-common \
    stress-ng \
    sysbench \
    iozone3 \
    iperf3 \
    openssh-server \
    iputils-ping \
    && rm -rf /var/lib/apt/lists/*

RUN mkdir -p /var/run/sshd
RUN mkdir -p /root/.ssh
RUN chmod 700 /root/.ssh

RUN ssh-keygen -t rsa -N '' -f /root/.ssh/id_rsa
RUN cp /root/.ssh/id_rsa.pub /root/.ssh/authorized_keys

RUN echo "StrictHostKeyChecking no" >> /etc/ssh/ssh_config
RUN touch /root/.ssh/known_hosts

RUN mkdir -p /shared

RUN mkdir -p /etc/hpcc
COPY HPL.dat /etc/hpcc/
RUN echo "node01 slots=1\nnode02 slots=1" > /etc/hpcc/hostfile

EXPOSE 22

ENV OMPI_ALLOW_RUN_AS_ROOT=1
ENV OMPI_ALLOW_RUN_AS_ROOT_CONFIRM=1

CMD ["/usr/sbin/sshd", "-D"] 