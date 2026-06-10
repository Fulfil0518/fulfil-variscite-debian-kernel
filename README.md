# Production Kernel versions

These tables keep track of which production kernel versions are usable and currently deployed.

These tables are in chronological order, with each release including previous changes. If in doubt, use the last entry of the table for a production kernel.

### v6.6
This version is kept alive on this [PR](https://github.com/Fulfil0518/fulfil-variscite-debian-kernel/pull/5)

| Version                                 | Description                                            | Commit / PR | Release Date |
| --------------------------------------- | ------------------------------------------------------ |--------|--------|
| 6.6.52-v6-baseline-ga097d4cb99b2        | Vanilla v6 kernel with MARS and LFP device trees       | [a097d4cb99b2](https://github.com/Fulfil0518/fulfil-variscite-debian-kernel/commit/a097d4cb99b2)  | Epoch |
| 6.6.52-prod.gantry.fix-gcb1a5007fb15    | Fix to MARS device tree to drive pin 50 to low <br>to prevent CAN disconnect for 4.2 gantry boards | [cb1a5007fb15](https://github.com/Fulfil0518/fulfil-variscite-debian-kernel/commit/cb1a5007fb15) <br> https://github.com/Fulfil0518/fulfil-variscite-debian-kernel/pull/27 | 2026/06/01 |


### v5.4

| Version                             | Description | Commit / PR |
| ----------------------------------- | ----------- | -------|
| 5.4.142-baseline-g11d2a3c8bf26      | Vanilla kernel with MARS and LFB device trees | [11d2a3c8bf26](https://github.com/Fulfil0518/fulfil-variscite-debian-kernel/commit/11d2a3c8bf26) <br> https://github.com/Fulfil0518/fulfil-variscite-debian-kernel/pull/1

Any production machine should be normally using the latest of these kernels. This can be inspected by `uname -r` or the [MARS dashboard](https://grafana.fulfil-api.com/d/bad24255-4cd5-411e-8380-c079e2076172/fw-mars-machine).

There are two major versions - v5.4 and v6.6. v5.4 is the go to stable release, but we are trying to migrate everything to v6.6 as it has significant stability improvements and is shown to alleviate SBC disconnects. Eventually we want to move off of v5.4 everywhere.

The versions strings in these tables can be used in a Ansible kernel-swap command:

`make kernel-swap LOCATION=[location] TARGET=[target] VERSION=0+[version-string]`

Or using apt when SSH'd inside the machine:

```
apt-get update
apt-get install imx8mn-debian-kernel=0+[version-string]
```

e.g. if version is 6.6.52-v6-baseline-ga097d4cb99b2, then do

`make kernel-swap LOCATION=[location] TARGET=[target] VERSION=0+6.6.52-v6-baseline-ga097d4cb99b2`

Going forward, try to prefix the version string with prod to distinguish it from other testing kernels. e.g. 6.6.52-prod.prevent.explosion-g[commit]



Linux kernel
============

There are several guides for kernel developers and users. These guides can
be rendered in a number of formats, like HTML and PDF. Please read
Documentation/admin-guide/README.rst first.

In order to build the documentation, use ``make htmldocs`` or
``make pdfdocs``.  The formatted documentation can also be read online at:

    https://www.kernel.org/doc/html/latest/

There are various text files in the Documentation/ subdirectory,
several of them using the Restructured Text markup notation.

Please read the Documentation/process/changes.rst file, as it contains the
requirements for building and running the kernel, and information about
the problems which may result by upgrading your kernel.
