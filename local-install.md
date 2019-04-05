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

* need to comment out eleasticsearch from config.yml
* Mac OSX: sqlite error (sqlite3 is installed via HomeBrew): 

```bash
pygeoapi generate-openapi-document -c local.config.yml > openapi.yml
/Users/just/project/ogg/wfs3/pygeoapi.git/pygeoapi/flask_app.py:49: YAMLLoadWarning: calling yaml.load() without Loader=... is deprecated, as the default Loader is unsafe. Please read https://msg.pyyaml.org/load for full details.
  CONFIG = yaml.load(fh)
/Users/just/project/ogg/wfs3/pygeoapi.git/pygeoapi/openapi.py:440: YAMLLoadWarning: calling yaml.load() without Loader=... is deprecated, as the default Loader is unsafe. Please read https://msg.pyyaml.org/load for full details.
  s = yaml.load(ff)
Traceback (most recent call last):
  File "/Users/just/project/ogg/wfs3/pygeoapi.git/pygeoapi/provider/geopackage.py", line 124, in __load
    conn.enable_load_extension(True)
AttributeError: 'sqlite3.Connection' object has no attribute 'enable_load_extension'

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "/Users/just/.pyenv/versions/pygeoapi37/bin/pygeoapi", line 11, in <module>
    load_entry_point('pygeoapi', 'console_scripts', 'pygeoapi')()
  File "/Users/just/.pyenv/versions/3.7.1/envs/pygeoapi37/lib/python3.7/site-packages/click/core.py", line 764, in __call__
    return self.main(*args, **kwargs)
  File "/Users/just/.pyenv/versions/3.7.1/envs/pygeoapi37/lib/python3.7/site-packages/click/core.py", line 717, in main
    rv = self.invoke(ctx)
  File "/Users/just/.pyenv/versions/3.7.1/envs/pygeoapi37/lib/python3.7/site-packages/click/core.py", line 1137, in invoke
    return _process_result(sub_ctx.command.invoke(sub_ctx))
  File "/Users/just/.pyenv/versions/3.7.1/envs/pygeoapi37/lib/python3.7/site-packages/click/core.py", line 956, in invoke
    return ctx.invoke(self.callback, **ctx.params)
  File "/Users/just/.pyenv/versions/3.7.1/envs/pygeoapi37/lib/python3.7/site-packages/click/core.py", line 555, in invoke
    return callback(*args, **kwargs)
  File "/Users/just/.pyenv/versions/3.7.1/envs/pygeoapi37/lib/python3.7/site-packages/click/decorators.py", line 17, in new_func
    return f(get_current_context(), *args, **kwargs)
  File "/Users/just/project/ogg/wfs3/pygeoapi.git/pygeoapi/openapi.py", line 441, in generate_openapi_document
    click.echo(yaml.safe_dump(get_oas(s), default_flow_style=False))
  File "/Users/just/project/ogg/wfs3/pygeoapi.git/pygeoapi/openapi.py", line 426, in get_oas
    return get_oas_30(cfg)
  File "/Users/just/project/ogg/wfs3/pygeoapi.git/pygeoapi/openapi.py", line 201, in get_oas_30
    p = load_plugin('provider', cfg['datasets'][k]['provider'])
  File "/Users/just/project/ogg/wfs3/pygeoapi.git/pygeoapi/plugin.py", line 89, in load_plugin
    plugin = class_(plugin_def)
  File "/Users/just/project/ogg/wfs3/pygeoapi.git/pygeoapi/provider/geopackage.py", line 69, in __init__
    self.cursor = self.__load()
  File "/Users/just/project/ogg/wfs3/pygeoapi.git/pygeoapi/provider/geopackage.py", line 127, in __load
    raise ProviderConnectionError()
pygeoapi.provider.base.ProviderConnectionError
Exception ignored in: <function GeoPackageProvider.__del__ at 0x106d5c6a8>
Traceback (most recent call last):
  File "/Users/just/project/ogg/wfs3/pygeoapi.git/pygeoapi/provider/geopackage.py", line 259, in __del__
    self.__unload()
  File "/Users/just/project/ogg/wfs3/pygeoapi.git/pygeoapi/provider/geopackage.py", line 184, in __unload
    self.cursor.execute("DROP TABLE IF EXISTS {}".format(self.view))
AttributeError: 'GeoPackageProvider' object has no attribute 'cursor'
```
