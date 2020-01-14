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

Used as `perf stat -e cs ls` to obtain context switch data about `ls`.

>### `-p`
Used to record events and analyse performance by supplying PIDs of the processes in a comma seperated list.

>### `-t`
Used to record events and analyse performance on existing thread IDs.

>### `-d`
Used to provide a ,more detailed performance analysis, consisting of time taken per event and so on.

>## 2. `cachegrind`

`cachegrind` simulates how your program interacts with a machine's cache hierarchy and (optionally) branch predictor. It simulates a machine with independent first-level instruction and data caches (I1 and D1), backed by a unified second-level cache (L2). This exactly matches the configuration of many modern machines.

However, some modern machines have three or four levels of cache. For these machines (in the cases where `cachegrind` can auto-detect the cache configuration) it simulates the first-level and last-level caches. The reason for this choice is that the last-level cache has the most influence on runtime, as it masks accesses to main memory. Furthermore, the L1 caches often have low associativity, so simulating them can detect cases where the code interacts badly with this cache.

Therefore, `cachegrind` is a tool for doing cache simulations and annotating your source line-by-line with the number of cache misses. In particular, it records:

*   L1 instruction cache reads and misses (I1)
*   L1 data cache reads and read misses, writes and write misses (D1)
*   L2 unified cache reads and read misses, writes and writes misses (LL)

## Usage

```bash
$ valgrind --tool=cachegrind <program>
```
 Cachegrind will slowly excecute the program and print summary cache statistics. It also collects line-by-line information in a file `cachegrind.out.pid`, where `pid` is the program's process id.

 ```bash
$ cg_annotate <filename>
```
The above is done to generate a function-by-function summary, and possibly annotate source files.

```bash
$ cg_merge -o outputfile <file1> <file2> <file3> ...
```
The above is done to read multiple profile files, as created by Cachegrind, merges them together, and writes the results into another file in the same format.

 The merging functionality might be useful if you want to aggregate costs over multiple runs of the same program, or from a single parallel run with multiple instances of the same program.

 ```bash
 cg_diff file1 file2
 ```
 cg_diff is a simple program which reads two profile files, as created by Cachegrind, finds the difference between them, and writes the results into another file in the same format.

 ## Common Options

 >## `--<cachename>=<size>,<associativity>,<line size>`

 Here `<cachename>` can be I1, D1 or L1 and this options is used to specify the size, associativity and line size of the cache level.

 >## `--cache-sim=no|yes [yes]`

 Enables or disables collection of cache access and miss counts.

 >## `-branch-sim=no|yes [no] `

Enables or disables collection of branch instruction and misprediction counts.By default this is disabled as it slows Cachegrind down by approximately 25%.

>## `--cachegrind-out-file=<file>`

Write the profile data to `file` rather than to the default output file, `cachegrind.out.pid`