# CephFS Performance Tests

This repository houses performance tests of CephFS.

* [Parallel Client Performance Test](./kernel-build/README.md)

## Future Tests

### Many Clients

| role    | count |
|:-------:|:-----:|
| mon     | 3
| osd     | 16
| mds     | 3
| clients | 100


many clients, 100, 200, 400, 800
figure out memory usage of MDS

open file test, scale with clients, examine memory usage

mass write test? mass read test?

listing directories?

millions of files

