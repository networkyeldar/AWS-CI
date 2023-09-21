# Building Continuous Integration(CI) pipeline using AWS Cloud9
This a demo video for creating CI on AWS

# Steps to run the project
* Create a repository on GitHub
* Open [AWS Cloud9](https://us-east-1.console.aws.amazon.com/cloud9control/home?region=us-east-1#/product)
* Create ssh-keys in AWS Cloud9

```ssh-keygen -t rsa```

* Upload ssh-keys to Github
* Create files for the project such as Makefile, requirements.txt, hello.py, and test_hello.py
  
```make Makefile```

```make requirements.txt```

```make hello.py```

```make test_hello.py```

* Create scaffolding for the project
  * Makefile

```
install:
	pip install --upgrade pip &&\
		pip install -r requirements.txt

test:
	python -m pytest -vv test_hello.py


lint:
	pylint --disable=R,C hello.py

all: install lint test
```

  * requirements.txt

```
pylint
pytest
```

* Create a python virtual environment and source it if not created

```
python3 -m venv ~/.myrepo
source ~/.myrepo/bin/activate
```

* Create initial ```hello.py``` and ```test_hello.py```

hello.py

```
def toyou(x):
    return "hi %s" % x


def add(x):
    return x + 1


def subtract(x):
    return x - 1
```

test_hello.py

```
from hello import toyou, add, subtract


def setup_function(function):
    print("Running Setup: %s" % {function.__name__})
    function.x = 10


def teardown_function(function):
    print("Running Teardown: %s" % {function.__name__})
    del function.x


### Run to see failed test
#def test_hello_add():
#    assert add(test_hello_add.x) == 12

def test_hello_subtract():
    assert subtract(test_hello_subtract.x) == 9
```

* Run ```make all``` which will install, lint and test code.
* Setup Github Actions in ```pythonapp.yml```
```
name: Python application test with Github Actions

on: [push]

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v2
    - name: Set up Python 3.5
      uses: actions/setup-python@v1
      with:
        python-version: 3.5
    - name: Install dependencies
      run: |
        make install
    - name: Lint with pylint
      run: |
        make lint
    - name: Test with pytest
      run: |
        make test
```
* Commit changes and push to Github
* Verify Github Actions Test Software
