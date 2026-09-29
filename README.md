CUDACycloneRandom — simple description

CUDACycloneRandom is a modified version of the CUDACyclone solver for Bitcoin puzzles, which searches for private keys in a pure random manner (each key chosen independently), not sequentially.

What it does

Searches for a Bitcoin private key (target hash160) within a given range

Chooses keys randomly with a PRNG (xorshift64star)

Computes each point using scalarMul (Jacobian + 4-bit window)

Speed: ~31 Mkeys/s on RTX 3060 

Compile 
make 

 
 ./CUDACyclone --range  20000000:3fffffff \
              --target-hash160 d39c4704664e1deb76c9331e637564c257d68a08\
              --random --seed 42 --grid 128,256

======== PHASE-1: BRUTEFORCE ==========================
RANDOM MODE ON (PURE), SEED = 42
TIME: 11.1 S | SPEED: 31.3 MKEYS/S | COUNT: 348532736 (PURE RANDOM)

======== FOUND MATCH! =================================
PRIVATE KEY   : 000000000000000000000000000000000000000000000000000000003D94CD64
PUBLIC KEY    : 030D282CF2FF536D2C42F105D0B8588821A915DC3F9A05BD98BB23AF67A2E92A5B
SAVED TO      : FOUND_KEY.TXT
