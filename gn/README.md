#

This directory contains the scripts to launch slurm containers on Tencent Cloud Cluster to support [cc_net](https://github.com/Oneflow-Inc/redpajama-data/tree/main/data_prep/cc/cc_net)

# How to use the images

```
docker pull registry.cn-beijing.aliyuncs.com/oneflow/slurm-head:latest
docker pull registry.cn-beijing.aliyuncs.com/oneflow/slurm-worker:latest
```

- master (on jump machine) 

```bash
docker run --rm --name slurm-head-$USER --network=host --add-host=slurmmaster:10.0.0.26 --add-host=slurmnode1:10.0.0.20 --user=admin registry.cn-beijing.aliyuncs.com/oneflow/slurm-head
```

- worker (on compute node)

```bash
docker run --rm --name slurm-worker-$USER --network=host --add-host=$(hostname):127.0.0.1 --add-host=slurmmaster:10.0.0.26 --add-host=slurmnode1:10.0.0.20 --user=admin -e SLURM_NODENAME="slurmnode1" registry.cn-beijing.aliyuncs.com/oneflow/slurm-worker
```

- stop

```bash
docker rm -f slurm-head-$USER
docker rm -f slurm-worker-$USER
```

# Use it on Guannian Tencent Cloud

```
launch_master.sh
```


NODENAME should be different on all involved machines.
```
env NODENAME=1 bash launch_workder.sh

```
