# jmweb-org

Small, well-made command-line tools for the daily workflow of machine learning
and AI engineers. Each does one thing, runs offline, returns honest exit codes,
and drops into CI. No services, no accounts, nothing to administer.

## Tools

- [gpu-gate](https://github.com/jmweb-org/gpu-gate) — Wait for a free GPU, claim
  it, set `CUDA_VISIBLE_DEVICES`, and run your command. The wait-pick-export-run
  loop for shared multi-GPU boxes without a cluster scheduler.
- [dsdiff](https://github.com/jmweb-org/dsdiff) — A git-style diff between two
  dataset files: schema changes plus column-level distribution drift (PSI), with
  a CI gate.
- [repro-manifest](https://github.com/jmweb-org/repro-manifest) — Capture a
  portable manifest of a run's environment, code, config and seeds, then diff
  two manifests to explain why two runs differed.
- [mlenv](https://github.com/jmweb-org/mlenv) — Snapshot the full ML stack
  (Python, CUDA, driver, torch build, GPUs, env vars) to one file and diff two
  snapshots.

## Design

The tools share a deliberate shape. Each is a single command that takes a file
or two and returns a verdict: a readable terminal view, `--json` for machines,
and a meaningful exit code. Most ship a `--check` mode that fails CI on the
change that matters, so they slot into a pipeline or a pre-commit hook without
adopting a platform. They are offline-first and dependency-light, and each is
small enough for one engineer to maintain.

## About

Maintained by José del Río, a machine learning engineer based in Madrid.
Personal projects and demos live on a separate account:
[github.com/delcenjo](https://github.com/delcenjo).
