# Minimal Python project

![Build status](https://img.shields.io/travis/com/energizah/minimal-python-project/master)

## How to use this

1. Create a file tree structure matching the one described below.

2. Create a local packages directory ("virtual environment" or "venv"). On Debian/Ubuntu you might need to first run `sudo apt install python3-dev python3-pip python3-venv` to get the `venv` and `pip` modules.

```
python3 -m venv myenv
```

3. Install your project into the venv in editable mode. Editable mode means you can make changes to your code without reinstalling (with the exception of `setup.py`. If you change that, you'll have to reinstall.).

```
myenv/bin/pip install -e .
```

4. Run the console script `greet` in the venv:

```
myenv/bin/greet
```

or run `__main__.py` as a module:

```
myenv/bin/python -m greetings
```


## Tree structure


The `python-greeter/` directory is called the "project root". That should be your shell's working directory whenever you're using this project.
```
python-greeter/setup.py
python-greeter/src/greetings/app.py
python-greeter/src/greetings/cli.py
python-greeter/src/greetings/__init__.py
python-greeter/src/greetings/__main__.py
```
### `setup.py`
```python
# setup.py

import pathlib

import setuptools

PROJECT_DIR = pathlib.Path(__file__).parent

DISTRIBUTION_PACKAGE_NAME = "hello"
VERSION = "0.1.0"
DESCRIPTION = "Greetings."
CONSOLE_SCRIPTS = ["greet = greetings.cli:cli"]


INSTALL_REQUIRES = (PROJECT_DIR / "requirements.in").read_text().splitlines()

setuptools.setup(
    name=DISTRIBUTION_PACKAGE_NAME,
    version=VERSION,
    description=DESCRIPTION,
    packages=setuptools.find_packages("src"),
    package_dir={"": "src"},
    include_package_data=True,
    install_requires=INSTALL_REQUIRES,
    entry_points={"console_scripts": CONSOLE_SCRIPTS},
)
```

### `app.py`
```python
# app.py

def morning():
    print('hello')


def evening():
    print('gooodbye')
```

### `cli.py`
```python
# cli.py
import click

from greetings import app


commands = [
    click.Command("morning", callback=app.morning),
    click.Command("evening", callback=app.evening),
]
cli = click.Group(commands={c.name: c for c in commands})
```

### `__init__.py`
```python
# __init__.py
# Yes, it's blank.
```

### `__main__.py`
```python
# __main__.py
from greetings import cli

cli.cli()
```

