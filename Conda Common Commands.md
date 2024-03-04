## Conda Common Commands

*continuously updated*

Some commonly used commands in Conda

### Conda

```bash
conda --version
```

```bash
conda update conda
```



### Env

```bash
conda env list
```

```bash
conda create --name env_name python=3.8
```

```bash
conda activate env_name
```

```bash
conda deactivate
```

```bash
conda remove --name env_name --all
```

```bash
conda remove --name env_name package_name
```

```bash
conda env export --name myenv > myenv.yml
```

```bash
conda env create -f myenv.yml
```



### Package

```bash
conda list
```

```bash
conda install package_name
```

```bash
conda install package_name -c conda_forge
```

```bash
conda update package_name
```

```bash
conda uninstall package_name
```

```bash
conda clean -p
conda clean -t
conda clean -y
```

go to `conda clean -h`

 
