## Slurm Directives Examples

Below are some examples of SLURM directives that can be used in your batch scripts in order to meet certain job requirements.

1. To run a 32-core job for 24 hours on a single Alpine CPU node:
```bash
#SBATCH --partition=amilan
#SBATCH --nodes=1
#SBATCH --ntasks=32
#SBATCH --time=24:00:00
```

2. To run a 56-core job (28 cores/node) across two Alpine CPU nodes in the low-priority qos for seven days:
```bash
#SBATCH --partition=amilan
#SBATCH --nodes=2
#SBATCH --ntasks-per-node=28
#SBATCH --time=7-00:00:00
#SBATCH --qos=long
```

3. To run a 16-core job for 24 hours on a single Alpine AMD GPU node, using all three GPU accelerators:
```bash
#SBATCH --partition=ami100
#SBATCH --nodes=1
#SBATCH --ntasks=16
#SBATCH --time=24:00:00
#SBATCH --gres=gpu:3
```

4. To run a 50-core job for 2 hours on a single Alpine NVIDIA GPU node, using 2 GPUs:
```bash
#SBATCH --partition=aa100
#SBATCH --nodes=1
#SBATCH --ntasks=50
#SBATCH --time=02:00:00
#SBATCH --gres=gpu:2
```

5. To run an 8-core job for 4 hours on any node that has at least 1 GPU:
```bash
#SBATCH --nodes=1
#SBATCH --ntasks=8
#SBATCH --time=4:00:00
#SBATCH --gres=gpu
```

#### Full Example Job Script

Run a 1-hour job on 4 cores on an Alpine CPU node with the normal qos that runs a python script using a custom conda environment.

```
#!/bin/bash

#SBATCH --partition=amilan
#SBATCH --job-name=example-job
#SBATCH --output=example-job.%j.out
#SBATCH --time=01:00:00
#SBATCH --qos=normal
#SBATCH --nodes=1
#SBATCH --ntasks=4
#SBATCH --mail-type=ALL
#SBATCH --mail-user=youridentikey@colorado.edu

module purge
module load anaconda
conda activate custom-env

python myscript.py
```

Alpine is jointly funded by the University of Colorado Boulder, the University of Colorado Anschutz, Colorado State University, and the National Science Foundation (award 2201538).

Couldn't find what you need? [Provide feedback on these docs!](https://forms.gle/bSQEeFrdvyeQWPtW9)
