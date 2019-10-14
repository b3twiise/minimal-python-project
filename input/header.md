# Minimal Python project

![Build status](https://img.shields.io/travis/com/energizah/minimal-python-project/master)

## How to use this

1. Create a file tree structure matching the one described below.

2. Create a local packages directory ("virtual environment" or "venv"). On Debian/Ubuntu you might need to first run `sudo apt install python3-dev python3-pip python3-venv` to get the `venv` and `pip` modules.

```
python3 -m venv myenv
```

3. Install your project into the venv in editable mode. Editable mode means you can make changes to your code without reinstalling. There are a couple of exceptions: if you change `setup.py` or create a new subpackage (subdirectory), you'll have to install again.

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
