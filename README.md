# This is very general HPC manual for beginners

## miniconda
Generally, you have to install miniconda in your home directory to create your own virtual environment
```sh
wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh

bash Miniconda3-latest-Linux-x86_64.sh -b 

```
## exit the terminal and open again

```sh

conda --version

```



## create new virtual enviroment

```sh
conda create -n myenv python=3.10
```


## if you have some old envs and you want to clone it here

```sh
conda create —-prefix /source/envs —clone /home/user/
```


## creating job script for HPC

```sh
#!/bin/bash
#SBATCH -t 2-00:00:00
#SBATCH -p gpu
#SBATCH -J test
#SBATCH --nodes=1
#SBATCH --gpus-per-node=1
#SBATCH --cpus-per-task=6
#SBATCH --mem=50G
#SBATCH -o ~/job_logs/train_%A_%a.out
#SBATCH -e ~/job_logs/train_%A_%a.err


# Set environmnet variables
export RESULTS_FOLDER="/projects/user/"

# Activate conda environment
source /home/USERNAME/miniconda3/bin/activate myenv

# Run python job

``` 

## run interactive jobs
```sh
srun --job-name=interactive_job \
     --output=interactive_job_%j.out \
     --error=interactive_job_%j.err \
     --time=02:00:00 \
     --partition=partition_name \
     --ntasks=1 \
     --cpus-per-task=4 \
     --mem=8G \
     --pty /bin/bash
```


## if you sbatch a job script and run a job in a certain node, you should be able to interactive ssh the node

```sh
ssh node
```

## common Q&A
