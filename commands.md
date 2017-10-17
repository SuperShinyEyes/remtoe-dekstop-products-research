```bash
ssh seyoung@130.233.195.77

loginctl unlock-sessions

# For a single TigerVNC session
ssh -L 5901:127.0.0.1:5901 -N -f -l parks1 130.233.97.35
ssh -L 5901:127.0.0.1:5901 -N -f -l seyoung 130.233.195.77
ssh -L 5901:127.0.0.1:5901 -N -f -l seyoung 130.233.193.163

ssh -L 5901:127.0.0.1:5901 -N -f -l cs-208

ssh cs-208 -L 5901:localhost:5901 -N -f
ssh cs-208 -L 5902:localhost:5902 -N -f

# For NoMachine free NX connection
ssh -L 4000:localhost:4000 -N -f -l seyoung 130.233.195.77
ps -ef | grep ssh

ssh git@admin.cs.hut.fi

# Following command doesn't need a separate SSH tunneling
# localhost:3 is the server host at port 5903.
# cs-208 is the HOST in .ssh/config
./vncviewer localhost:3 -via cs-208
```


```bash
slurm history

# 1 day 0 hour. Default: 15 min.
srun --mem=50G --time=1-0 python pi.py

srun --cpus=10 --mem=50G --time=1-0 --test-only

# real(walltime), user(CPU time), sys(walltime - CPU time)
time python tset.py

srun -pty python

# See all available modules
module avail

module load anaconda3
srun --pty ipython
srun --pty -p interactive ipython



# Run Matlab
sinteractive
module load matlab
matlab

# Creating a batch
vim name.slrm
sbatch name.slrm
slurm q
# Result: name-jobID.out

```

# Sbatch script
```bash
#!/bin/bash
#SBATCH --mem=10G
#SBATCH --time=1:00:00
#SBATCH -J JobName
#SBATCH -o outputName

```

## Start server
```bash
./vncserver -SecurityTypes=TLSPlain -PlainUsers=$USER -pam_service login -desktop
              $HOSTNAME
```

## 
```bash

```

## 
```bash

```

## 
```bash

```

## 
```bash

```

## 
```bash

```

## 
```bash

```
