
# Starter Project Template

Use this repo to start a new project. 

You likely want to **download** and not clone or fork. Then you can `git init` and start a new repo. 

![Download project](tmp/gitlab-download.png)


Follow the steps below to configure and initialize.

## Setup

* Run `cd scripts; sh config.sh` (or `config.bat`)
* Setup `app/_ins.sql` with the correct Workspace & App Number
* Decide if your project will use a static or dynamic template `_release_template_static.sql` or `_release_template_dynamic.sql`.  You could optionally delete one of them.
* Generate for your `_release.sql` script [ASCII Art](https://asciiartgen.now.sh/?style=standard)
* Optionally remove directories that won't apply (ie. conversion)

## Getting Started

Start a new release:
* Run commands like the following depending on a static or dynamic release

```
rm ../release/[a-z]*.sql
cp ../release/_release_template_static.sql.sql ../release/_release.sql
```


```
rm ../release/[a-z]*.sql
cp ../release/_release_template_dynamic.sql.sql ../release/_release.sql
```


* Optionally modify `script/new.sh` as needed

```
sh scripts/new.sh
```


## Folder Structure

| Folder | Description |
|:--|--|
| apex | Application exports
| bin | Binary files, executable scripts, Sublime/VSC specific files 
| conversion | Conversion and/or seed data scripts
| data | Seed data scripts
| docs | Project documents 
| install | Installation scripts of none code objects like tables, types, and indexes.
| lib | Installation libraries (OSS, Logger, etc..)
| release | Current release scripts for changes and patching
| scripts | Usually re-runable scripts referenced by a release script
| packages | Packages (`.pls` & `.plb` or `.pks` & `.pkb`), triggers (not audit triggers) or sometimes stand alone procedures and functions.
| sql | Generic sql scripts that are not part of the application
| tmp | Garbage stuff, not under version control
| synonyms | Application Synonyms
| triggers | Application Triggers
| views | Application views
| www | Assets that go in the server: images, CSS, and JavaScript

## Release Autocomplete

_Note: This script was developed intnerally by Insum Solutions_

**Status: POC**

This node.js application will automatically add files in the `views` and `packages` directory into a release file.

### Release File Configuration

You must make sure that the following is included in your release file:

```sql
-- AUTOREPLACE_START
-- AUTOREPLACE_END
```

The code will automatically fill in the section between these lines.

### Run

`node ./release/release.js ./release/<release file>`


Example:

```bash
# Go to releases folder in trunk/master of current SVN/Git project
cd releases

node release.js _release.sql
```

This application can be run multiple times as it keeps the substitution strings.
