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

>## 2. `cachegrind`

`cachegrind` simulates your program's interaction with the machine's cache hierarchy and (optionally) branch predictor. It tracks usage of the simulated first-level instruction and data caches to detect poor code interaction with this level of cache; and the last-level cache, whether that is a second- or third-level cache, in order to track access to main memory. As such, programs run with Cachegrind run twenty to one hundred times slower than when run normally. 

## Installation (On Linux)   HAVE TO CHECK FOR THIS!

```bash
$ uname -r       ```5.0.0-37-generic```
$ sudo apt install linux-tools-5.0.0-37-generic
```
Use the first command to obtain the kernel release, and fill it in the second command.

## Usage

To run Cachegrind, execute the following command, replacing 'program' with the program you wish to profile with Cachegrind:

```bash 
$ valgrind --tool=cachegrind program
```

The statistics that will be generated via this command are : 

* First-level instruction cache reads (or instructions executed) and read misses, and last-level cache instruction read misses;
* Data cache reads (or memory reads), read misses, and last-level cache data read misses;
* Data cache writes (or memory writes), write misses, and last-level cache write misses;
* Conditional branches executed and mispredicted; and
* Indirect branches executed and mispredicted.

Cachegrind then prints summary information about these statistics to the console, and writes more detailed profiling information to a file (cachegrind.out.pid by default, where pid is the process ID of the program on which you ran Cachegrind).
This file can be further processed by the accompanying cg_annotate tool, like so:

```bash
$ cg_annotate cachegrind.out.pid
```

In order to compare the profile files created by Cachegrind and to see the difference in program performance before and after a change , the cg_diff command, is used as follows :

```bash
$ cg_diff <initial profile output file> <subsequent profile output file>
```

## Common subcommands 

Cachegrind supports a number of options to focus its output. Some of the options available are: 

>### `--I1`

Specifies the size, associativity, and line size of the first-level instruction cache, separated by commas: --I1=size,associativity,line size

>### `--D1`

Specifies the size, associativity, and line size of the first-level data cache, separated by commas: --D1=size,associativity,line size

>### `--LL`

Specifies the size, associativity, and line size of the last-level cache, separated by commas: --LL=size,associativity,line size

>### `--cache-sim`

Enables or disables the collection of cache access and miss counts. The default value is yes (enabled). 

>### `--branch-sim`

Enables or disables the collection of branch instruction and misprediction counts. This is set to no (disabled) by default, since it slows Cachegrind by approximately 25 per-cent. 




