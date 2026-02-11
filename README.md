# Description

**any2eln** is a tool to extract data from any Electronic Laboratory Notebook (ELN) software, to a `.eln` archive.

This `.eln` archive can then easily be re-imported in another ELN.

# Supported sources

* [Labfolder](#labfolder-module) (functional)
* Labguru (coming soon)
* Scinote (coming soon)
* Benchling (coming soon)

# Installation

~~~
git clone https://github.com/TheELNConsortium/any2eln
cd any2eln

poetry install
~~~

# Usage

~~~
poetry run python any2eln --help
~~~

# Labfolder module

## Description

This module allows you to extract all accessible data from a Labfolder account. It goes through all the entries and saves them per author as `.eln` archives. Using this module requires an account on a Labfolder instance.
Optionally it allows filtering by subgroup, for this group id and subgroup id have to entered. 

The `DATA` elements are converted as `.csv` sheet by sheet, when possible, and the full `.json` metadata is also saved alongside.

## Disclaimer

This project is not affiliated with Labfolder software or Labforward GmbH. It simply leverages the [publicly documented API](https://labfolder.labforward.app/api/v2/docs/development.html#notebook-entries) to add a feature: export everything as `.eln`.

## Usage

~~~
poetry run python any2eln --src labfolder
~~~

Subgroups can be checked via. 
```shell
TOKEN='Authorization: Bearer <TOKEN>'
curl 'https://labfolder.mpi-cbg.de/api/v2/groups/150/subgroups?limit=50'  -H 'Accept: */*' -H $TOKEN -H 'Accept-Encoding: br'
```

The exported data will be saved in the current directory in a folder named `export-Y-m-d-H-M-s`.

For a more verbose output, add ``DEV=1`` to your execution environment.

## Caveats

If there is an error downloading a file for some reason, the error will be logged but the script will continue. Use verbose output (``DEV=1``) to have more information logged.

# License

This piece of software is under [MIT license](./LICENSE).
