BUGS
====

* BUG: "python perf timeit --compare-to=pypy" doesn't tune correctly the runner
  for pypy. pypy requires more warmup samples (10) than cpython (1).
* BUG: --duplicate of timeit must be ignored in PyPy, see the discussion
  on the speed mailing list.


Blocker issues for perf 1.0 stable API
======================================

* store metadata common to all benchmarks at the root in JSON


TODO
====

* Need to write unit test for Runner.timeit()
* load(): remove '-' special case
* add stdev() method, maybe median_stdev()
* Calibration run: display time per iteration and total duration
* system:

  * advice: use --affinity when no CPU is isolated
  * set the CPU scaling governor when intel_pstate is not used.
    Use "userland" governor with a fixed CPU speed (max speed)?
  * warn if HyperThread is enabled?
  * check that isolated CPU "respect HyperThreading" (are part of the
    same physical cores)
  * check that rcu_nocbs respects isolated CPUs
  * detect NUMA

* compare: check also if benchmarks are unstable
* External tool (?) to produce nice HTML reports:

  * https://magic.io/blog/uvloop-blazing-fast-python-networking/

    - HTML, JS: d3 graphic library
    - min, max, std dev
    - https://github.com/MagicStack/pgbench
    - https://github.com/MagicStack/vmbench

  * http://hdrhistogram.github.io/HdrHistogram/
  * probability density graphs

    - https://hydra.snabb.co/build/589970/download/2/report.html
    - https://en.wikipedia.org/wiki/Probability_density_function
    - enhance hist_scipy.py to support more than one benchmark
    - https://docs.scipy.org/doc/scipy/reference/tutorial/stats.html

* Runner: add a compare methods to compare N benchmarks
* Add TextRunner.timeit()
* doc: clarify difference between compare & compare_to
* doc: more CLI examples
* doc: timeit, mention -o option
* timeit compare: write result as JSON into one or two files?
* metadata: voluntary_ctxt_switches and nonvoluntary_ctxt_switches of
  /proc/self/status? or/and read /proc/interrupts to count interruptions?
* Pass Python arguments to subprocesses like -I, -O, etc.
* "venv/pypy5.0-ec75e7c13ad0/bin/python -m perf timeit -w0 -l1 -n 10 pass -v --worker"
  sometimes create a sample equals to 0
* Write unit test for compare_to --group-by-speed
* Write unit test for tracemalloc and track memory: allocate 30 MB,
  check usage >= 30 MB
* Remove BenchmarkSuite.__iter__()?


Low priority
============

* compare: display metadata
* fix hist if benchmark only contains one sample
* support --fast + -p1
* perf CLI: handle FileNotFoundError for input file (need unit test)
* convert --remove-outliers: more serious algorithm? or configurable percent?
