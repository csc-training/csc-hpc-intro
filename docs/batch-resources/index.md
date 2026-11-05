# Batch job resource usage

!!! abstract "Goals of this module"

    After this module you can:

    - check how much CPU, memory and time your finished jobs actually used
    - spot failed or badly sized jobs and adjust their resource requests
    - explain how resource usage turns into billing units on Roihu and LUMI

??? abstract "Slides"

    <iframe src="../slides/06_understanding_usage.html" loading="lazy"
        style="width:100%; aspect-ratio:16/9; border:0" allowfullscreen></iframe>
    [Open fullscreen](../slides/06_understanding_usage.html){ target=_blank }

    The LUMI-specific slides are placed below the corresponding Roihu slides
    (press :arrow_down: or use the arrows in the corners).

## Why it matters

Supercomputers are shared by hundreds of users. Everything your job reserves
(cores, memory, GPUs) is unavailable to others while the job runs, and your
project is billed for it whether it was used or not. Usually one resource runs
out first: a job that reserves all the memory of a node blocks the remaining
cores, even if it only uses one of them.

The workflow is the same on every Slurm system:

1. Run a short test job with your best guess of the resources.
2. Check what the job actually used with `seff` and `sacct`.
3. Adjust the requests and repeat until the efficiencies are high.

It is fine if a job occasionally fails because of too small a request. It is
much worse to always request far too much "just in case".

## Roihu and LUMI

Both Roihu and LUMI use Slurm, so `sacct` works the same way on both. The main
differences are in billing and in the partitions:

=== "Roihu"

    - Billing: CPU, GPU and Storage billing units (BU). Memory is billed
      separately from cores.
    - Check your project's usage with `csc-projects`.
    - [Billing in Docs CSC](https://docs.csc.fi/computing/hpc-billing/)

=== "LUMI"

    - Billing: CPU core-hours, GPU-hours and storage TB-hours. On the `small`
      partition you are billed for cores *or* for memory in 2 GB chunks per
      core, whichever is larger. On `standard` and `standard-g`, whole nodes are
      billed.
    - Check your project's usage with `lumi-allocations`.
    - [Billing in the LUMI documentation](https://docs.lumi-supercomputer.eu/runjobs/lumi_env/billing/)

## Tutorials

- [Using `sacct` and `seff`](sacct-seff-tutorial.md): run a small array job
  and find out why some of its sub jobs fail.
- [Exercise: overview of your recent jobs](sacct-seff-exercise.md)

## Going further

- Docs CSC: [How much memory does my job need?](https://docs.csc.fi/support/faq/how-much-memory-my-job-needs/)
  and the [performance checklist](https://docs.csc.fi/computing/running/performance-checklist/)
- LUMI: [Slurm quickstart](https://docs.lumi-supercomputer.eu/runjobs/scheduled-jobs/slurm-quickstart/)
  and [partitions](https://docs.lumi-supercomputer.eu/runjobs/scheduled-jobs/partitions/)
