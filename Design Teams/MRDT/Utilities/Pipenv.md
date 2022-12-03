# Pipenv
Pipenv is a combination of multiple python libraries that allows one command for all stages of the work cycle.

It automates dependency management replacing 'requirement.txt' with 'Pipfile'
Handles dependency resoltuion as well. Makes venvs easy to use. 

Here we create a venv if it doesn't already exist. 
```shell
pipenv shell
``` 

Installation of libraries is as easy as
```shell
pipenv install numpy
```

All dependencies are consolidated in a single Pipfile.
To lock your dependencies do:
```shell
pipenv lock
```
This creates a Pipfile.lock that stores the dependency requirements

To use the pipfile.lock over pipfile do
```shell
pipenv install --ignore-pipfile
```

Run a command in venv without starting a shell
```Shell
pipenv run <command>
```

