# Job Shop Schedule Problem (JSSP)

[![CircleCI](https://circleci.com/gh/mcfadd/Job_Shop_Schedule_Problem/tree/master.svg?style=svg)](https://circleci.com/gh/mcfadd/Job_Shop_Schedule_Problem/tree/master)
[![Documentation Status](https://readthedocs.org/projects/job-shop-schedule-problem/badge/?version=latest)](https://job-shop-schedule-problem.readthedocs.io/en/latest/?badge=latest)

#### Version 0.2.0  

JSSP is an optimization package for the Job Shop Schedule Problem.  
JSSP has two different optimization algorithms:  

1. Parallel Tabu Search
2. Genetic Algorithm

For more information on JSSP, [read the docs](https://readthedocs.org/projects/job-shop-schedule-problem/).

### How to Install

1. [Download JSSP-0.2.0.linux-x86_64.egg](https://github.com/mcfadd/Job_Shop_Schedule_Problem/releases/download/0.2.0/JSSP-0.2.0.linux-x86_64.egg)
2. Run `easy_install JSSP-0.2.0.linux-x86_64.egg`

**For Developers**

After clone this repo, change directories to where `setup.py` exists and run 
```
pip install --upgrade pip
pip install -r requirements.txt
python setup.py build_ext
```
If you get an error about `python.h` not being found try installing [python3-dev](https://stackoverflow.com/questions/31002091/what-is-python-dev-package-used-for).

### How to Use

After installation, JSSP can imported as a normal python package.  

**Important Note**

Job-Tasks in jobTasks.csv and sequenceDependencyMatrix.csv need to be in ascending order according to (job_id, task_id).  
(see csv files in the [data](https://github.com/mcfadd/Job_Shop_Schedule_Problem/tree/master/data/given_data) folder for reference)

### Example

The following example minimally demonstrates how to run parallel tabu search to find a solution to the problem instance in [data/given_data](https://github.com/mcfadd/Job_Shop_Schedule_Problem/tree/master/data/given_data).

```python
from JSSP.solver import Solver
from JSSP.data import Data

# initialize data
data_directory = 'data/given_data'
Data.initialize_data_from_csv(data_directory + '/sequenceDependencyMatrix.csv',
                              data_directory + '/machineRunSpeed.csv',
                              data_directory + '/jobTasks.csv')

# run tabu search
solver = Solver()
solution = solver.tabu_search_iter(iterations=500,
                                   num_processes=4,
                                   tabu_list_size=20,
                                   neighborhood_size=250,
                                   )
# print solution
print(solution)

# create Schedule.xlsx in 'output' directory
solution.create_schedule_xlsx_file('output')                   
```

**Flexible Job Shop**

To read in a flexible job shop problem instance from a .fjs file (see [data](https://github.com/mcfadd/Job_Shop_Schedule_Problem/tree/master/data/fjs_data) folder) do the following:
```python
from JSSP.data import Data

Data.initialize_data_from_fjs('data/fjs_data/Barnes/Barnes_mt10c1.fjs')
```

## How to Contribute

If you would like to contribute to this project please see [CONTRIBUTING.md](https://github.com/mcfadd/Job_Shop_Schedule_Problem/blob/master/CONTRIBUTING.md).

## License

JSSP is licensed under the [ISC License](https://github.com/mcfadd/Job_Shop_Schedule_Problem/blob/master/LICENSE):
```text
ISC License

Copyright (c) 2019, Matthew McFadden

Permission to use, copy, modify, and/or distribute this software for any
purpose with or without fee is hereby granted, provided that the above
copyright notice and this permission notice appear in all copies.

THE SOFTWARE IS PROVIDED "AS IS" AND THE AUTHOR DISCLAIMS ALL WARRANTIES
WITH REGARD TO THIS SOFTWARE INCLUDING ALL IMPLIED WARRANTIES OF
MERCHANTABILITY AND FITNESS. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR
ANY SPECIAL, DIRECT, INDIRECT, OR CONSEQUENTIAL DAMAGES OR ANY DAMAGES
WHATSOEVER RESULTING FROM LOSS OF USE, DATA OR PROFITS, WHETHER IN AN
ACTION OF CONTRACT, NEGLIGENCE OR OTHER TORTIOUS ACTION, ARISING OUT OF
OR IN CONNECTION WITH THE USE OR PERFORMANCE OF THIS SOFTWARE.
```
