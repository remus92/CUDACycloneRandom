# ⚡ CUDACycloneRandom

A modified version of **CUDACyclone** that adds a **pure random** search mode — every key is chosen independently, with no EC chain and no sequential order.

---

## 🎯 What it does

- Searches for a Bitcoin private key (**target hash160**) inside a given range
- Picks keys **randomly** using a PRNG (`xorshift64star`)
- Computes each point with an optimized `scalarMul` (**Jacobian coordinates + 4-bit window**)
- Saves the found key to `found_key.txt`

---

## 📊 Performance

| Mode             | Speed (RTX 3060) | Coverage        |
|------------------|------------------|-----------------|
| **Pure random**  | **~31 Mkeys/s**  | probabilistic   |

> Pure random is ~30× slower by design — every key requires a full `scalarMul` (~3600 modular ops), while the sequential mode uses an EC chain (~15 ops/key).

---



## 🖥️ Example — Pure Random with fixed seed

**Command:**
```bash
./CUDACyclone --range 20000000:3fffffff \
              --target-hash160 d39c4704664e1deb76c9331e637564c257d68a08 \
              --random --seed 42 --grid 128,256

Random mode ON, seed = 42
======== PrePhase: GPU Information ====================
Device               : NVIDIA GeForce RTX 3060 (compute 8.6)
SM                   : 28
ThreadsPerBlock      : 256
Blocks               : 4096
Points batch size    : 128
Batches/SM           : 256
Batches/launch       : 64 (per thread)
Memory utilization   : 2.7% (328.2 MB / 11.8 GB)
-------------------------------------------------------
Total threads        : 1048576

======== Phase-1: BruteForce ==========================
Random mode ON (pure), seed = 42
Time: 11.1 s | Speed: 31.3 Mkeys/s | Count: 348532736 (pure random)

======== FOUND MATCH! =================================
Private Key   : 000000000000000000000000000000000000000000000000000000003D94CD64
Public Key    : 030D282CF2FF536D2C42F105D0B8588821A915DC3F9A05BD98BB23AF67A2E92A5B
Saved to      : found_key.txt


📦 Full setup
apt update;
apt-get install -y joe;
apt-get install -y zip;
apt-get install -y screen;
apt-get install -y curl libcurl4;
apt-get install build-essential;
apt-get install -y gcc;
apt-get install -y make;
apt install cuda-toolkit;
apt-get install -y joe zip screen curl libcurl4 build-essential gcc make && \
apt install -y cuda-toolkit && \
git clone https://github.com/remus92/CUDACycloneRandom.git && \
cd CUDACycloneRandom && \
make
