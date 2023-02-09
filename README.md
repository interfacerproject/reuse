<!--
SPDX-License-Identifier: AGPL-3.0-or-later
Copyright (C) 2023 Dyne.org foundation <foundation@dyne.org>

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU Affero General Public License as
published by the Free Software Foundation, either version 3 of the
License, or (at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU Affero General Public License for more details.

You should have received a copy of the GNU Affero General Public License
along with this program.  If not, see <https://www.gnu.org/licenses/>.
-->

# About the project

This project is intented to be used with Interfacer projects to
apply appropriate licensing information on all files of a project.


## Usage

The usage is very human.  You include this repository as a submodule
to your project as the path `.reuse`.  This can be achieved by
running:

	git submodule add https://github.com/interfacerproject/reuse .reuse

Then, you can commit and push your changes, such as:

	git commit -m 'add reuse support'
	git push

After you include the repository, you can use
[the Reuse tool](https://reuse.software/) with the provided templates.


### Annotating all files

With this repository included into your project, run the sh(1) script:

	.reuse/annotate -y2022-2023 src/*.c doc/*.md

from your project working directory with parameters you want to
supply to the Reuse tool.

Most oftenly, you'll only need to supply the year and the files to
be annotated.  The year is supplied either with `-y` or `--year`,
which can take a list of comma-seprated years, range of years, or
a year.

You can supply `-r` or `--recursive` to recursively annotate a
directory, which can be the current directory, `.`, as well.  Using
this might result in mismatches with the Reuse tool if it can't
detect the file type of a file.  In that case, you can supply the
`--skip-unrecognised` flag to skip those files temporarily, and
then annotate them separately with `-s` or `--style` option, which
takes an argument such as `c`, `css`, or `python`.  The possible
style options can be optained by running `-h` or `--help`.

In this example:

	.reuse/annotate -y2023 -spython scripts/sh-script-without-extension

`-s` uses Python-style comments on a shell script without an
extension.

The script works as long as it is relatively referenced, since it
uses your current working directory when called to locate the files.


### Downloading the licenses

After you annotated all your files, you must run

	.reuse/download

to download all the licenses used in your project.  This will create
a `LICENSES/` directory and put all the downloaded licenses there.
After this step is done, you should remove any individual `LICENSE`
file found in your project root.

Then, you should be all good to go and comply with the Reuse spec.
To verify that, you can run:

        .reuse/lint

which will tell you any errors if they're present.
