# Parallel Client Performance Test

These tests evaluate the performance of single and multiple MDS servers when
handling requests from multiple clients. These clients are building the kernel:
first unpacking the source, compiling the kernel, and finally removing all
source and compiled files.

These tests are run using [ceph-ansible](http://github.com/ceph/ceph-ansible)
on [Linode](http://linode.com) virtual machines. Each test uses 3 monitors, 3
MDSs (2 standby during single MDS tests), 16 OSDs, and 8 or 16 clients. All VMs
use the basic 2048MB plan on Linode (i.e. 2GB RAM, 1 core). The one exception
is tests using the 4096MB MDS servers (4GB RAM, 2 cores).

## Summary

The time to execute the parallel build for the clients is given in the table below:

| RAM/Cores | # of Clients | # of MDSs | Time | Average Sum of Client Latency |
|:---------:|:------------:|:---------:| ----:| -----------------------------:|
| 2GB/1     | 8            | 1         | 99m  | 3326.75                       |
| 2GB/1     | 8            | 2         | 80m  | 1364.04                       |
| 2GB/1     | 8            | 3         | 63m  | 1307.50                       |
| 2GB/1     | 16           | 1         | 323m | 16633.70                      |
| 2GB/1     | 16           | 2         | 263m | (lost: corrupt db)            |
| 2GB/1     | 16           | 3         | 84m  | 2499.43                       |
| 4GB/2     | 8            | 1         | 68m  | 2037.89                       |
| 4GB/2     | 8            | 2         | 73m  | 1235.29                       |
| 4GB/2     | 8            | 3         | 50m  | 847.45                        |
| 4GB/2     | 16           | 1         | 147m | 5277.31                       |
| 4GB/2     | 16           | 2         | 115m | 3274.02                       |
| 4GB/2     | 16           | 3         | 108m | 2876.89                       |

When using a single core, the single MDS would consistently be at 100% CPU for
the duration of the test for all configurations. With 2 cores, the single MDS
would use approximately 150% CPU for the duration of the test. (Numbers about
CPU usage were not collected. I observed this using htop.)

A full list of configurations and some graphs of performance metrics are
[here](./configs.md).
