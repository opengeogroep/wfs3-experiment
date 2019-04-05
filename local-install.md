# 
## Installatie

### Get Code
```bash
git clone https://github.com/geopython/pygeoapi.git  pygeoapi.git
```

### Setup Python3 VirtualEnv

Try with Python 3.7.1.

```bash

# Using virtualenv
virtualenv -p python pygeoapi
cd pygeoapi.git
. bin/activate

# Using pyenv
pyenv virtualenv 3.7.1 pygeoapi37
pyenv activate pygeoapi37

```

### Install

```bash
cd pygeoapi.git
pip install --upgrade pip
pip install -r requirements.txt
pip install -r requirements-dev.txt
pip install -e .

```

### Configure

```bash
cp pygeoapi-config.yml local.config.yml
# edit local.config.yml
# TODO: what is most important to edit?
export PYGEOAPI_CONFIG=/Users/just/project/ogg/wfs3/pygeoapi.git/local.config.yml
# generate OpenAPI Document
pygeoapi generate-openapi-document -c local.config.yml > openapi.yml
export PYGEOAPI_OPENAPI=/path/to/openapi.yml
pygeoapi serve
```

## Findings

* 