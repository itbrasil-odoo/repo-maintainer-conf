# IT Brasil repo maintainer configuration

This repo contains configuration files to automatically setup teams and repositories in the IT Brasil organization.

## How it works
When a config change is merged, a Github action will use the [repo-maintainer tool](https://github.com/itbrasil-odoo/repo-maintainer)
to update or create teams and repositories and to generate the documentation.

Documentation is hosted on https://itbrasil-odoo.github.io/repo-maintainer-conf/

## Conf structure

In the `conf` folder you'll find a `psc` folder and a `repo` folder.
Each of them contains YAML files. Each file contains the configuration for one or more team/repo.
The tool does not care about the name of the file or if the file contains 1 or 100 items.
What matters is that we keep them organized by "category" or "app" as it is now.

NOTE: current files where generated mostly automatically.
If you think that any of them has not the right name or a piece of content is misplaced,
feel free to propose a PR to fix it.

## Global conf and checksum

Two files should never be touched:

* `conf/global.yml`: hosts general configuration
* `conf/checksum.yml`: hosts the checksum of each file.

The checksum is computed and updated on each build
to ensure that repos and teams will be updated only if necessary.

## How to add a new repo

1. look for the right category file in the `repo` folder
2. if not present, create one
3. add the conf for the new repo, like:
```
account-analytic:  # repo slug
  branches:  # branches to setup
    - "14.0"
    - "15.0"
    - "16.0"
  category: Account  # used for documentation
  default_branch: "14.0"  # setup default branch
  name: Odoo account analytic related addons  # user friendly name
  psc: accounting-maintainers  # maintainers PSC/team
  psc_rep: core-maintainers-psc-representative  # maintaners representative team
```
4. commit, push and open a PR against this repo

## How to update a repo

Simply modify any of the parameters above, commit, push and open a PR.

## How to add a new PSC

1. look for the right category file in the `psc` folder
2. if not present, create one
3. add the conf for the new psc, like:
```
accounting-maintainers:
  members:
    - user1
    - user2
    - userN
  name: Accounting maintainers
  representatives:
    - user4
    - user5
accounting-maintainers-psc-representative:
  members:
    - user6
  name: Accounting maintainers psc representative
  representatives: []
```

## How to update a PSC

Simply modify any of the parameters above, commit, push and open a PR.
