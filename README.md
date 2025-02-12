# Website builder [![Build Status](https://travis-ci.com/homieiot/convention-website.svg?branch=master)](https://travis-ci.com/homieiot/convention-website)

This repository contains the static website generator for the [Homie Website](https://homieiot.github.io).
The build is triggered by a change in any of the Homie specification respositories
and performed by Travis CI. The resulting webpage is uploaded to 
https://github.com/homieiot/homieiot.github.io/tree/master and is served by GitHub.

The generator in use is [Hugo](https://gohugo.io/).

You can just call the `./build.sh` script within this directory
and find the page in the output directory `site`.

## Manually generate the webpage

You need Hugo in the extended version (with sass/scss support).

The git grab utility requires python3. For a non-root environment,
it is recommended to create a python virtual environment:

```sh
python3 -m venv dependencies
source dependencies/bin/activate
```

Install the dependencies `gitpython`, `pyyaml`,
then run the git grab utility and and hugo last:

```
pip install -r requirements.txt
./grabrepos.py
hugo
```

## Upload a manually generated webpage

The webpage lives within the "master" branch of https://github.com/homieiot/homieiot.github.io/tree/master.
The generated "site" directory need to be pushed to that branch.

```
cd site
git init
git remote add origin git@github.com:homieiot/homieiot.github.io.git
git add .
git commit -m "Manually generated webpage"
git push origin -f HEAD:master
```

## Data: FAQ, Maintainers

You find data files in the `data/` directory. At the moment this is the FAQs
and the maintainers file in yaml format.

## Generated content files

All files in `content/specification/` are automatically generated by the tool `grabrepos.py`.
A file for each tagged version of the Homie Core convention is generated. Only those sections
are considered that are mentioned in the `multiversion.yml` configuration file.

Preface documents, that are valid for all versions, are extracted from the `develop` branch and
prefaced on every document by the Hugo generator.

## Maintainer

Website maintainer: David Graeff <david.graeff@web.de>
