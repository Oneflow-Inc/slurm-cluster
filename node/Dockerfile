# FROM ubuntu:20.04
FROM thufeifeibear/ccnet:v0.4

RUN apt update -y && apt install munge -y && apt install vim -y && apt install build-essential -y && apt install git -y && apt-get install mariadb-server -y && apt install wget -y

ARG DEBIAN_FRONTEND=noninteractive
RUN apt install slurmd slurm-client -y
RUN apt install sudo -y && useradd -m admin -s /usr/bin/bash -d /home/admin && echo "admin:admin" | chpasswd && adduser admin sudo && echo "admin     ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

COPY slurm.conf /etc/slurm-llnl/
COPY cgroup.conf /etc/slurm-llnl/
COPY docker-entrypoint.sh /etc/slurm-llnl/
COPY munge.key /etc/munge/munge.key
RUN chmod 600 /etc/munge/munge.key && chgrp munge /etc/munge/munge.key && sudo chown munge /etc/munge/munge.key

EXPOSE 6817 6818 6819

RUN apt update -y && apt install libopenmpi-dev -y && pip3 install mpi4py submitit

ENTRYPOINT ["/etc/slurm-llnl/docker-entrypoint.sh"]
