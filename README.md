# indigitall-test

Indigitall Backend test for company admission. 

## Contents

This project is composed of the following main components:

1. `extraction_transformation.ipynb`: The jupyter notebook that solves the first part of the exercise.
2. `/architecture_design`: Contains all the files needed for the second part of the exercise.
   1. `.pdf`: The final submission in a easy to read format.
   2. `.md` The final submission in an editable format.
   3. `.png`: The diagram in an easy to read format.
   4. `.xml`: The editable diagram. It can be loaded into [draw.io](https://draw.io).

## Install requirements

### Get Python

We are using version 3.7.2. Any 3.7 version should work, get the latest.

- [Download link](https://www.python.org/downloads/)

### Install requirements

We recommend using virtual environments to create an isolated environment for the application.

1. Download virtualenv package: `pip install virtualenv`
2. Create a virtualenv in the project directory: `virtualenv indigitall_env`
3. Activate the virtualenv in the command prompt that will be used to execute the scripts:
   - Windows: `.\indigitall_env\Scripts\activate`

To install the requirements:

1. go to the directory where the `requirements.txt` can be found
2. Execute: `pip install -r requirements.txt`

## Execution

To start a Jupyter notebook server  in current directory execute:  `jupyter notebook`. Your browser should open with a UI that allows you to open any notebook in that dir. [More info](https://jupyter-notebook-beginner-guide.readthedocs.io/en/latest/execute.html)

## Architecture diagram

To edit the architecture diagram, `architecture_design.xml` can be loaded in [this](draw.io) website.