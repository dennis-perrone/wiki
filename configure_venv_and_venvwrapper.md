# Configure Python Virtual Environments and Virtualenvwrapper

## Notes

- Add the following lines to `~/.bashrc.d/env_vars.sh`

```bash
export WORKON_HOME=$HOME/.virtualenvs
export PROJECT_HOME=$HOME/development/scripts/python
export VIRTUALENVWRAPPER_SCRIPT=/usr/bin/virtualenvwrapper.sh
source /usr/bin/virtualenvwrapper.sh
```

- Run the following commands:

```bash
mkdir ~/.virtualenvs
source ~/.bashrc
```

- All the virtual environments created using virtualenvwrapper will now be stored in `./virtualenvs`.
- To create new virtual environment:
  - Python3:

  ```bash
  mkvirtualenv <project-name>
  ```
  
  - Python 2:

  ```bash
  mkvirtualenv --python=python2 <project name>
  ```

- The virtualenv will automatically activate after creation

- Install packages local to the python3 virtualenv (and not global to the system) using

```bash
pip3 install <package-name>
```

- Install packages local to the python2 virtualenv (and not global to the system) using

```bash
pip install <package-name>
```

- To exit the virtualenv

```bash
deactivate
```

- To get back into the virtualenv

```bash
workon <project-name>
```

## References

1. [Gist: Python3, Pip3, Virtualenv, and Virtualenvwrapper Setup](https://gist.github.com/IamAdiSri/a379c36b70044725a85a1216e7ee9a46)
