# MeshMiner

A cryptocurrency miner for **HomeScrypt** (Lumenite v1.1 and v1.2). Runs on your
NVIDIA GPU, your CPU, or both. Point it at any pool.

## Download

| Platform | File |
|----------|------|
| Windows 10 / 11 | `meshminer-win.zip` |
| Linux (64-bit)  | `meshminer-linux.zip` |

## Run

Unzip, set your wallet in the included `start-lumenite-v12` script, and run it.
Or from a terminal:

```
meshpool-miner --pool <host:port> --user <your-address>.<worker> --backend both --algo v12
```

`--backend` is `cuda`, `cpu`, or `both`.

## Dev fee

**0.5%**, or **0.1%** when mining on `meshpool.net`. Shown in the startup banner.

## Requirements

- **GPU:** NVIDIA RTX 20-series or newer, with a current driver. No CUDA toolkit needed.
- **CPU:** any 64-bit machine.
- **OS:** Windows 10/11 or 64-bit Linux.

Antivirus flags mining software by default. Add an exclusion for the folder if needed.
