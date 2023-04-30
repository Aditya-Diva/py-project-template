# Py Project Template

[![Github License](https://img.shields.io/badge/License-MIT-green?style=plastic)](LICENSE)

[![GitHub Workflow Staging](https://img.shields.io/github/actions/workflow/status/Aditya-Diva/Py-Project-Template/python-cicd-staging.yml?style=plastic&label=Staging%20CI)](https://github.com/Aditya-Diva/Py-Project-Template/actions/workflows/python-cicd-staging.yml)
&emsp;
[![GitHub Workflow Production](https://img.shields.io/github/actions/workflow/status/Aditya-Diva/Py-Project-Template/python-cicd.yml?style=plastic&label=Main%20CI)](https://github.com/Aditya-Diva/Py-Project-Template/actions/workflows/python-cicd.yml)

[![Code Style](https://img.shields.io/badge/Code_Style-black-black?style=plastic)](https://pypi.org/project/black/)
&emsp;
[![Linting](https://img.shields.io/static/v1?label=Linting&message=pylint&color=brightgreen&style=plastic)](https://pypi.org/project/pylint/)

Check out project links:

[![Docs](https://img.shields.io/badge/Docs-sphinx-blue?style=plastic)](https://aditya-diva.github.io/Py-Project-Template/)
&emsp;
[![Testing](https://img.shields.io/badge/Testing-pytest-orange?style=plastic)](https://aditya-diva.github.io/Py-Project-Template/reports/pytest/index.html)
&emsp;
[![Docs](https://img.shields.io/badge/Coverage-pytestcov-blue?style=plastic)](https://aditya-diva.github.io/Py-Project-Template/reports/pytest-cov/index.html)

## Table of Contents

- [About the Project](#about-the-project)
- [Packages Used](#packages-used)
- [Usage](#usage)
  - [Installation](#installation)
  - [Running the Application](#running-the-application)
  - [To Develop](#to-develop)
- [Overall Flow](#overall-flow)
  - [Linting](#linting)
  - [Testing](#testing)
    - [PyTest Reports](#pytest-reports)
    - [Coverage Reports](#coverage-reports)
  - [Pre-commit](#pre-commit)
  - [Documentation](#documentation)
  - [Deployment](#deployment)
  - [Additional](#additional)
- [Contributing](#contributing)
- [License](#license)
- [Contact](#contact)

## About The Project

This is a sample template for python projects that i'd like to update from time to time as i learn more in python development.

It's also meant to act as a refresher for some good practices and/or to look up basic how-to.

It involves some concepts like abstract classes, documentation, and testing and implements a rather limited calculator logic for the base.

## Flow Packages used

- **pipenv** for creating a virtual environment.
- **pytest** for testing packages. (https://docs.pytest.org/)
- **pre-commit** for linting(**pylint**) and running tests(**pytest**) before committing.
- **pytest-html** to generate pytest html report.
- **pytest-cov** to generate test coverage reports.
- **sphinx** for maintaining auto generated code documentation along with links to generated reports mentioned above.

## Usage

### Installation

```sh
$ sudo apt-get install -y python3-pip
$ pip3 install pipenv
```

With newer Python versions, go to [Pipfile](Pipfile), and update,

```pipfile
[requires]
python_version = "3.x"
```

And for support in Ubuntu 22.04,

```sh
export PATH="$HOME/.local/bin:$PATH" # pip3 installs have been shifted to the following location!

# Generally would end up giving -> AttributeError: module 'collections' has no attribute 'MutableMapping'
export SETUPTOOLS_USE_DISUTILS=stdlib # Handles import issues
```

### Running the Application

To use Py-project-template, first:

```sh
$ git clone https://github.com/Aditya-Diva/py-project-template
$ cd Py-Project-Template/
```

To drop into the interactive terminal for the environment:

```
$ pipenv shell
$ pipenv install # rm Pipfile.lock, to regenerate package versions if required
$ python3 main.py

# FOR REFERENCE:
$ pipenv --rm # To remove the virtual env created (if necessary)
```

Else to run directly:

```sh
$ pipenv run python3 main.py
```

### To Develop

Install the dev packages

```
$ pipenv install --dev
```

## Overall Flow

Let's look into different components in brief.

To drop into the virtual environment, please refer to [Usage](#usage).

---

### Linting

> **Lint**, or a linter, is a static code analysis tool used to flag programming errors, bugs, stylistic errors and suspicious constructs. Here we use [**pylint**](https://pypi.org/project/pylint/).

To ignore file(s):

> Added the following at the top of [conf.py](docs/source/conf.py) to ignore this file since it's generated by sphinx and would rather keep its current format.

```py
# pylint: disable-all
```

Pylint settings file can be generated with:

```sh
pylint --generate-rcfile >> .pylintrc
```

> In this settings file the boilerplate can be editted to ignore conditions such as 'deprecated-decorator' and 'protected-access' warnings from pylint in [.pylintrc](.pylintrc)
> Protected member functions were called directly during testing, hence being forcefully ignored.

---

### Testing

For testing, we're using [**pytest**](https://pypi.org/project/pytest/).

For testing:

```sh
$ cd tests
$ pytest
```

For quiet mode:

```sh
$ pytest -q
```

For marked testing:

```
$ pytest -m <mark_name>
E.g
$ pytest -m getter
```

Note :

- Different custom marks have been defined in [tests/pytest.ini](tests/pytest.ini)

#### **PyTest Reports**

- **[PyTest-HTML](https://pypi.org/project/pytest-html/)** used in [reports/update.sh](reports/update.sh) to create an HTMl report for pytest.

#### **Coverage Reports**

Using following packages:

- **[Coverage](https://pypi.org/project/coverage/)** - Code Analysis tool to determine which lines are executable/executed.
- **[PyTest-Cov](https://pypi.org/project/pytest-cov/)** - Test Coverage reports (Uses coverage internally)

> Please refer to [reports/.coveragerc](reports/.coveragerc) which acts as the config for test coverage.

> Please refer to [reports/update.sh](reports/update.sh) for understanding reports update steps.

In order to update reports,

```sh
$ pipenv shell
(env) $ ./reports/update.sh
```

OR

```sh
$ pipenv run ./reports/update.sh
```

---

### Pre-commit

[**Pre-commit**](https://pre-commit.com/) is used to trigger checks before a successful commit through hooks.

Refer to [.pre-commit-config.yaml](.pre-commit-config.yaml)

> Runs some basic checks on files, along with black formatter, pylint and finally pytest. These are run before user tries to commit and enforces standards.

To run this explicitly without having to commit:

```sh
$ pipenv shell
(env) $ chmod +x pre-commit.sh
(env) $ ./pre-commit.sh
```

---

### Documentation

> [**Sphinx**](https://www.sphinx-doc.org/en/master/) was used for documentation. Refer to live documentation for the project at <https://aditya-diva.github.io/Py-Project-Template/>

> Please refer to [docs/update.sh](docs/update.sh) for understanding docs update steps.

In order to update docs,

```sh
$ pipenv shell
(env) $ ./docs/update.sh
```

OR

```sh
$ pipenv run ./docs/update.sh
```

---

### Git Workflow

Please refer to [.github/workflows/python-cicd.yml](.github/workflows/python-cicd.yml).

Generally a better idea to use scripts(.sh files / .bat etc.) and run them in workflows but have used individual steps for an example. Using scripts can help with local testing as well.

---

### Deployment:

- On target system create a requirements.txt:

  ```sh
  $ pipenv requirements > requirements.txt
  $ pipenv requirements --dev-only > dev-requirements.txt
  ```

  While deploying, inside a virtualenv I run:

  ```sh
  $ pip3 install -r requirements.txt
  ```

- A similar setup can be created with Docker instead for containerization.

---

### Additional:

Some miscellaneous packages used are:

- **[Logging](https://docs.python.org/3/library/logging.html)** to maintain logs.
- **[Pydantic](https://pypi.org/project/pydantic/)** to standardize/validate inputs.
  - Pydantic has been used in [lib/utils/startup.py](lib/utils/startup.py) for validation in this repo. It could be used more thoroughly in python libraries as well.
- **[Dotenv](https://pypi.org/project/python-dotenv/)** to read .env settings/config.

## Contributing

Any contributions made are greatly appreciated.

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## License

Distributed under the MIT License. See [`LICENSE`](LICENSE) for more information.

## Contact

Aditya Divakaran - [@LinkedIn](https://www.linkedin.com/in/aditya-divakaran/) - [@Github](https://github.com/Aditya-Diva) - [@GMail](adi.develops@gmail.com)

Notes:

- This was tested on Ubuntu 22.04 and Windows (WSL).
- Refer to [notes](notes.txt) for helpful links on particular framework/tool.
