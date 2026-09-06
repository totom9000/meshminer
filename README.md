# MeshMiner

A miner for HomeScrypt (Lumenite v1.1 and v1.2). Runs on your NVIDIA GPU, your
CPU, or both. Point it at any pool.

## Download

From the [Releases](../../releases) page:

| Platform | File |
|---|---|
| Windows 10 / 11 | `meshminer-win-<version>.zip` |
| Linux (64-bit) | `meshminer-linux-<version>.tar.gz` |
| HiveOS | `meshpool-miner-<version>.tar.gz` |
| Docker | `bawls/meshminer:<version>` |

## Run

Unzip, set your wallet in the included `start-lumenite-v12` script, and run it.
Or from a terminal:

    meshpool-miner --pool <host:port> --user <your-address>.<worker> --backend cuda --algo v12

`--backend` is `cuda`, `cpu`, or `both`. `--device 0,1` picks specific cards;
by default every card is used.

With Docker:

    docker run --rm --gpus all -e WALLET=<your-address> -e WORKER=rig1 bawls/meshminer:<version>

## First start

The miner measures each card once, which takes about half a minute per card,
and remembers the result. Every card in a rig is measured on its own — cards
that report the same model name are not always the same card.

    meshpool-miner --tune-only     measure and exit; needs no pool or wallet
    meshpool-miner --retune        measure again

Retune after a driver update, a memory overclock, or a new version of the
miner. A stale result costs a few percent quietly.

## If your hashrate looks low, check the fan first

This is the single largest thing that can go wrong, and it does not look like a
fault — the miner runs, finds shares, and reports a number.

If the miner says fan control needs administrator, act on it. An RTX 5090 left
that way sat at 82 °C with its fan at 33% and sustained 3500 H/s. The same card
with `--fan auto` held its clock at 60 °C and did 7684.

Either run the miner elevated so its own curve applies, or pass `--fan auto`
and let the driver handle it.

## Dev fee
**1.2%, or 0.5% when mining on meshpool.net.** Shown in the startup banner.

It is accounted as a debt rather than a duty cycle: every second of your mining
accrues 1.2% of a second of fee, paid in one stint when it accumulates. Short
sessions carry the debt forward instead of escaping it, and long ones are never
charged more than the rate.

## Requirements

- **GPU:** NVIDIA Turing (RTX 20-series) or newer, with a current driver. No
  CUDA toolkit needed.
- **CPU:** any 64-bit machine.
- **OS:** Windows 10/11, or 64-bit Linux with glibc 2.35 or newer
  (Ubuntu 22.04+).

Antivirus flags mining software by default. Add an exclusion for the folder if
needed.
