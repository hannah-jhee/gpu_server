# gpu_server
## ssh config
In your local computer, modify your `~/.ssh/config` by appending these lines:
```
Host gpu
    HostName xxx.xx.xx.xx   # contact Hannah to see the ip address
    User user  # your ID
    ProxyCommand ssh physics -W %h:%p
```
You may not need `ProxyCommand`, so check it out by yourself.

## Environmental Modules
Currently available modules are
 - consistent-trees/1.0.1
 - cuda/11.2
 - fsps/3.2
 - gsl/2.7.1
 - hdf5/1.10.8
 - hyperion/0.9.10
 - mpich/
   - 2.1.5
   - 3.0.2
 - openmpi/4.0.3
 - rockstar-galaxies/0.9.9

You can load modules by running:
```
user@gpusystem:~$ module load mpich/2.1.5
```
These modules are installed at `/usr/local`. If you wish to install other packages, you can contact to Hannah. Otherwise, just install at your local `home` directory without `sudo`.

## Shared conda system
Miniconda3 is installed at `/usr/local/miniconda3`. It is recommended to run initially 
```
user@gpusystem:~$ /usr/local/miniconda3/bin/conda init
```
when you first log in, and it will write down conda initializing commands to your `~/.bashrc`. Then you will see `(base)` appearing in front of your ID on terminal such as:
```
(base) user@gpusystem:~$ 
```

### Conda Environments
There are several conda environments shared at `/usr/local/miniconda3/envs`.
#### `powderday`
In order to use `Powderday` or other related features such as `hyperion`, `statmorph`, etc., you have to run this command in shell:
```
(base) user@gpusystem:~$ module load fsps/3.2
(base) user@gpusystem:~$ module load hdf5/1.10.8
(base) user@gpusystem:~$ module load mpich/2.1.5
(base) user@gpusystem:~$ conda activate powderday
(powderday) user@gpusystem:~$ 
```
If `conda` command cannot be found, use `/usr/local/miniconda3/bin/conda` instead of `conda`. Or as suggested above, first run
```
$ /usr/local/miniconda3/bin/conda init
```
#### creating your own environments
If you'd like to create your own conda environments, run this command:
```
(base) user@gpusystem:~$ conda create --prefix=/home/<user>/.conda/envs/<env_name> python=x.x
```
`<user>` is your ID and `<env_name>` is the name of environment you want to create. Set the python version to the required one (i.e. 3.8). `--prefix` option is important.

### Running Jupyter Lab
Jupyter Lab or Jupyter Notebooks can be run remotely without browsing, and you can port-forward. Below is how to do this:
1. Run this command at remote server, with the port as you wish.
   ```
   (base) user@gpusystem:~$ jupyter lab --no-browser --port=8080
   ```
   You can find the token to get to the Lab. Copy it.
2. Run this command at your local computer.
   ```
   $ ssh -NL 8080:localhost:8080 gpu
   ```
3. At your local browser, type `localhost:8080` to get to Jupyter Lab.
4. Paste the token you have copied at 1.
