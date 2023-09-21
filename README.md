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
