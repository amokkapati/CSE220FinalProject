## How to Run in Scarab Container

### Step 1: Copy files into the container

```bash
docker cp perceptron.h cse220_$USER:/home/$USER/scarab/src/bp/perceptron.h
docker cp perceptron.cc cse220_$USER:/home/$USER/scarab/src/bp/perceptron.cc
docker cp bp.h cse220_$USER:/home/$USER/scarab/src/bp/bp.h
docker cp bp.c cse220_$USER:/home/$USER/scarab/src/bp/bp.c
docker cp bp_table.def cse220_$USER:/home/$USER/scarab/src/bp/bp_table.def
docker cp bp.param.def cse220_$USER:/home/$USER/scarab/src/bp/bp.param.def
```

### Step 2: Build Scarab

```bash
docker exec -it cse220_$USER /bin/bash
cd /home/$USER/scarab/src
make opt
```

### Step 3: Run simulations with the perceptron predictor

Pass `--bp_mech perceptron` to enable it:

```bash
./run.sh -o /Users/$USER/cse220_home -s 220 -e <experiment_name>
```

In your `lab.json` configurations:
```json
"configurations": {
    "perceptron": "--bp_mech perceptron",
    "bimodal":    "--bp_mech bimodal"
}
```

---

## Parameters

| Parameter | Default | Description |
|-----------|---------|-------------|
| `--perceptron_entries` | 512 | Number of perceptrons in the table |
| `--perceptron_hist_len` | 24 | Branch history length |
| `--perceptron_weight_bits` | 8 | Bits per weight (-128 to 127) |

Override defaults by adding to your configuration string:
```json
"perceptron_custom": "--bp_mech perceptron --perceptron_hist_len 32"
```