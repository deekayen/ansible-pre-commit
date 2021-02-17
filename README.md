Ansible pre-commit practice
========

This repository is meant to practice the installation and use of the [pre-commit](https://pre-commit.com/) utility.


Installation
---------

First, install pre-commit following the [instructions](https://pre-commit.com/#installation) from pre-commit.com.

### Linux

    $ pip install pre-commit

### MacOS

Using [homebrew](https://brew.sh/):

    $ brew install pre-commit

Usage
-----

Clone this repository:

    git clone git@github.com:deekayen/ansible-pre-commit.git

Then install the git pre-commit hooks

    $ cd ansible-pre-commit
    $ pre-commit install

Try it
------

Add a line to this README file or a task to the `playbook.yml`, then try to make a local commit.

    $ git add .
    $ git commit -m "Test pre-commit hooks."

The pre-commit utility will take a few moments on the first run to clone the `ansible-lint` repository and install its dependencies. After it does, it will take a few moments to lint the playbook file and should find a fatal linting problem:

```
Ansible-lint.............................................................Failed
- hook id: ansible-lint
- exit code: 2

WARNING  Listing 1 violation(s) that are fatal
unnamed-task: All tasks should be named
playbook.yml:6 Task/Handler: ping

You can skip specific rules or tags by adding them to your configuration file:
# .ansible-lint
warn_list:  # or 'skip_list' to silence them completely
  - unnamed-task  # All tasks should be named
Finished with 1 failure(s), 0 warning(s) on 1 files.
```

Note in your local git history that the commit did not save any changes and that your git stage should still have files pending. This error says that the `ping` task should have a `name` on it. Examine the `playbook.yml` and see how this new task would resolve the error.

```
  tasks:
    - name: Do a connection test.
      ping:
```

Add the `name` line to the `ping` task and try the commit again. The second run should go much faster, since `ansible-lint` is now already locally installed and the commit should be successful.
