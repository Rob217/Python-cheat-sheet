# Conda

## Environments

#### List environments
```bash
conda info --envs
```

#### Activate/deactivate environment
```bash
conda activate env_name
(env_name) conda deactivate
```

#### Create environment
```bash
conda create -n env_name python=3.8
```

#### Delete environment
Be sure to deactivate environment first.
```bash
conda env remove -n env_name
```
