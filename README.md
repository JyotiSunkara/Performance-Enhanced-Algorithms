# Churu-Darth-Romance

## Objective 

> Optimising code for matrix multiplication and merge sort, as well as gaining understanding of optimization methods and tools.

## Task 0

Gain an understanding of `​perf`, `cachegrind`, `gprof` and `clock_gettime​`.

>## 1. `perf`

`perf` is a performance counter tool for Linux that provides a framework for all things for performance analysis. It covers harware level (CPU/PMU) features as well as software features such as software counters, tracepoints.

Makes use of data from the Performance Monitoring Unit (PMU) in CPUs. 



## Installation (On Linux)

```bash
$ uname -r       ```5.0.0-37-generic```
$ sudo apt install linux-tools-5.0.0-37-generic
```
Use the first command to obtain the kernel release, and fill it in the second command.

## Common subcommands

>### `stat`

Used to run a command and obtain performance counter statistics on it.

For example `perf stat ls` gives us:
~ Add image here ~

>### `record`

Used to run a command and gather a performance counter profile from it that is stored into perf.data file without displaying anything. 

>### `report`

Used to read the perf.data file present in the directory and display the performance profile onto the terminal.

>### `list`

Used to list all the symbolic even types analysed by the `perf` command such as cache misses, context swiitches, L1-dcache-loads and so on.

>### `trace`

Used to show the events associated with the target,initially syscalls, but other system events like pagefaults, task lifetime events, scheduling events and so on.

## Common options

>### `-a`

Used to obtain a system wide performance analysis from all CPUs

>### `-e`

Used to show only data/ performance with respect to specific syscalls or events like context switches.

Used as `perf stat -e cs` to obtain context switch data.

>### `-p`

Used to record events and analyse performance by supplying PIDs of the processes in a comma seperated list.

>### `-t`

Used to record events and analyse performance on existing thread IDs.

>### `-d`

Used to provide a ,more detailed performance analysis, consisting of time taken per event and so on.
