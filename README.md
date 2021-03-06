[![Build Status](https://travis-ci.org/woudc/woudc-qa.png?branch=master)](https://travis-ci.org/woudc/woudc-qa)
[![Build status](https://ci.appveyor.com/api/projects/status/02koln2pe4ap5kvd/branch/master?svg=true)](https://ci.appveyor.com/project/tomkralidis/woudc-qa)
[![Downloads this month on PyPI](https://img.shields.io/pypi/dm/woudc-qa.svg)](http://pypi.python.org/pypi/woudc-qa)
[![Latest release](https://img.shields.io/pypi/v/woudc-qa.svg)](http://pypi.python.org/pypi/woudc-qa)
[![License](https://img.shields.io/github/license/woudc/woudc-qa.svg)](https://github.com/woudc/woudc-qa)

# WOUDC Quality Assessment library

Python package for automatically quality assessing [WOUDC](http://woudc.org) data based on defined rules.

## Installation

### Requirements

woudc-qa requires Python 2.7.

### Dependencies

See `requirements.txt`.

### Installing the Package

```bash
# via distutils
pip install -r requirements.txt
python setup.py install
```

## Usage

### Command line interface
```bash
usage: woudc-qa.py [-h] --file FILE

Execute Qa.

optional arguments:
  -h, --help   show this help message and exit
  --file FILE  Path to extended CSV file to be quality assessed.
```

## Examples
```python
from woudc_qa import qa
file_s = open(<path to your extended CSV file.>).read()
qa_results = qa(file_s)
# qa_results is a dictionary as such:
# qa_results: {
#     filename: {
#        test_id: {
#            row : {
#                result: result of this test, pass/fail/None/NR,
#                table: table name,
#                table_index: table_index,
#                element: element name,
#                related_test_id: test_id,
#                related_test_result: related tests result, pass/fail/None/NR
#                precond : precondition result: pass/fail/None/NR
#            }
#        }
#    }
# }
# where,
# 'filename' is the name of the file, default it to 'file1'
# 'test_id' is the test identifier from the test definition
# 'row' is the row number of the element under assessmet. Always 1 for non profile/payload element
# 'result', is the result of the assessment for the element at the indicated row for the given test
# 'table' is the name of the table where the element under assessment is found
# 'table_index' is the index of the above table. Default to 1, index will be incremented by 1 to handle multicipity
# 'element' is the element under assessment
# 'related_test_id' is a listing of any related test to this test
# 'related_test_result' is a aggregated result of all related tests to this test
# 'precond' is the aggregated result of any precondition checks
#
# from collections import OrderedDict
# test_result = qa_result[<filename>][<test_id>]
# iterate over test results by row:
# for row, result in test_result.iteritems():
#    print row, result
# get result of assessment at a specific row
# row_result = qa_results[<filename>][<test_id>][<row number>]['result']

```


## Development

For development environments, install
in a Python [virtualenv](http://virtualenv.org):

```bash
virtualenv foo
cd foo
. bin/activate
# fork master
# fork http://github.com/woudc/woudc-qa on GitHub
# clone your fork to create a branch
git clone https://github.com/{your GitHub username}/woudc-qa.git
cd woudc-qa
# install dev packages
pip install -r requirements.txt
python setup.py install
# create upstream remote
git remote add upstream https://github.com/woudc/woudc-qa.git
git pull upstream master
git branch my-cool-feature
git checkout my-cool-feature
# start dev
git commit -m 'implement cool feature'
# push to your fork
git push origin my-cool-feature
# issue Pull Request on GitHub
git checkout master
# cleanup/update once your branch is merged on GitHub
# remove branch
git branch -D my-cool-feature
# update your fork
git pull upstream master
git push origin master
```

### Running Tests

```bash
# via distutils
python setup.py test
# manually
python run_tests.py
# report test coverage
coverage run --source woudc_qa setup.py test
coverage report -m
```

### Code Conventions

woudc_qa code conventions are as per
[PEP8](https://www.python.org/dev/peps/pep-0008).

```bash
# code should always pass the following
find -type f -name "*.py" | xargs flake8
```

## Issues

All bugs, enhancements and issues are managed on
[GitHub](https://github.com/woudc/woudc-qa/issues).

## History

## Contact

* [Thinesh Sornalingam](http://geds20-sage20.ssc-spc.gc.ca/en/GEDS20/?pgid=015&dn=CN%3Dthinesh.sornalingam%40canada.ca%2COU%3DDAT-GES%2COU%3DMON-STR%2COU%3DMON-DIR%2COU%3DMSCB-DGSMC%2COU%3DDMO-CSM%2COU%3DEC-EC%2CO%3DGC%2CC%3DCA)
