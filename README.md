# CPU Cache Latency Profiler

**Status:** Planned
**Projected timeline:** August 1–15, 2027 for the Intel measurements
**First system:** Intel Core i7-9850H in my HP ZBook
**Second system:** AMD Ryzen 7 9800X3D once my desktop is built
**Tools:** C++, Python, and Matplotlib

## What I’m building

I want to see whether I can estimate a processor’s cache sizes by timing memory reads. I’ll write a C++ benchmark where each address contains the location to read next. The processor has to finish one read before it knows where to go.

I’ll begin with 4 KiB of data and work up to 256 MiB. As the data takes up more space, I’ll look for increases in the time it takes to complete each read.

## How I’ll run it

1. Build one shuffled chain that visits every intended location before repeating.
2. Pin the benchmark to one CPU core and warm up each data size.
3. Traverse the chain repeatedly and record nanoseconds per read.
4. Run a sequential traversal as a comparison.
5. Plot the results and collect more samples around any sharp changes.

I’ll record the compiler, build flags, node spacing, power settings, and number of trials so someone else can repeat the experiment.

## What I’m testing

My main question is which cache boundaries I can identify from timing alone. I’ll mark the transitions I see before comparing them with the processor’s published cache sizes. If the curve has a jump I can’t explain or a boundary I can’t see, I’ll document it.

## Timeline

- **August 1 - 7:** Build and validate the benchmark, then collect the first Intel measurements.
- **August 8 - 15:** Repeat the runs, investigate transitions, and publish the Intel graph.
- **Ryzen follow-up:** Run the same source and settings on my 9800X3D when the desktop is ready.

## Results I plan to publish

An annotated graph with data size on the horizontal axis and nanoseconds per read on the vertical axis, plus the raw CSV files. The Ryzen follow-up will add a second curve so both systems can be compared using the same experiment.

## Planned folders

- `src/` - C++ benchmark
- `tests/` - checks that the chain visits every intended location
- `scripts/` - commands to run the sweep and generate plots
- `docs/` - benchmark method and machine settings
- `results/` - raw data and graphs for each CPU
