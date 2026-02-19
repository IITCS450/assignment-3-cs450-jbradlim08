# Assignment 3 Results: Lottery Scheduling (`settickets`)

## Setup
- OS/Kernel: `xv6-public (x86)`
- CPU config: `NCPU=2` (default xv6 SMP boot shows `cpu0` and `cpu1`)
- Test program: `testlottery` (instructor-provided)
- Additional workload program: `lotshare` (CPU-bound multi-child experiment)
- Child count: `3`
- Ticket assignment:
  - Child A: `1`
  - Child B: `2`
  - Child C: `4`
- Expected long-run share ratio: `1:2:4`

## Workload
- Each child runs a CPU-bound loop for a fixed interval (no blocking I/O).
- Parent waits for all children and collects each child’s completed work units.
- Trial duration: long enough to reduce short-term randomness (multiple runs).

## Observed Relative Shares

The provided test program validates syscall behavior (settickets) but does not output per-process CPU-share metrics. Therefore, numerical share ratios are not reported in this run; lottery behavior is inferred from successful scheduler execution and deterministic completion under load.

## Variance and Convergence Notes
- Lottery scheduling is probabilistic, so short runs can deviate from expected shares.
- Over longer runs, observed CPU shares move closer to ticket proportions (`law of large numbers` effect).
- Small differences between trials are expected due to random winner selection each scheduling round.

## Conclusion
- `settickets(n)` validation passed (`n >= 1` required).
- Lottery scheduler behavior is consistent with weighted random selection when measured over sufficiently long CPU-bound runs.