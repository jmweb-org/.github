# jmweb-org

Small, well-made command-line tools for the daily workflow of machine learning
and AI engineers. Each does one thing, runs offline, returns honest exit codes,
and drops into CI. No services, no accounts, nothing to administer.

## Data

- [dsdiff](https://github.com/jmweb-org/dsdiff) — A git-style diff between two
  dataset files: schema changes plus column-level distribution drift (PSI), with
  a CI gate.
- [splitcheck](https://github.com/jmweb-org/splitcheck) — Detect rows that leak
  between train, validation and test splits, exact and after normalization, and
  fail CI when they do.
- [pii-sweep](https://github.com/jmweb-org/pii-sweep) — Scan dataset files for
  personally identifiable information, with a confidence per column and a CI
  gate, before the data leaves your hands.

## Environment and reproducibility

- [mlenv](https://github.com/jmweb-org/mlenv) — Snapshot the full ML stack
  (Python, CUDA, driver, torch build, GPUs, env vars) to one file and diff two
  snapshots.
- [repro-manifest](https://github.com/jmweb-org/repro-manifest) — Capture a
  portable manifest of a run's environment, code, config and seeds, then diff
  two manifests to explain why two runs differed.
- [gpu-gate](https://github.com/jmweb-org/gpu-gate) — Wait for a free GPU, claim
  it, set `CUDA_VISIBLE_DEVICES`, and run your command. The wait-pick-export-run
  loop for shared multi-GPU boxes without a cluster scheduler.

## Evaluation

- [evalgate](https://github.com/jmweb-org/evalgate) — Decide whether an eval
  delta is a real regression or sampling noise, and fail CI only when it is real.
- [slicemap](https://github.com/jmweb-org/slicemap) — Find the data slices where
  a new model regressed against an old one, ranked by how many rows are affected.

## Serving and cost

- [servectl](https://github.com/jmweb-org/servectl) — Serve a model file over
  HTTP in one command, with health and Prometheus metrics built in.
- [tokenmeter](https://github.com/jmweb-org/tokenmeter) — Count tokens and
  estimate cost for prompts before you send them, from the command line or as a
  CI budget gate.

## Design

The tools share a deliberate shape. Each is a single command that takes a file
or two and returns a verdict: a readable terminal view, `--json` for machines,
and a meaningful exit code. Most ship a `--check` mode that fails CI on the
change that matters, so they slot into a pipeline or a pre-commit hook without
adopting a platform. They are offline-first and dependency-light, and each is
small enough for one engineer to maintain.
