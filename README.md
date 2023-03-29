# multi-git-sync
A tool to sync multiple repos on different resources (e.g. github and gitlab).

Use it to automatically push each repo from one of the resources like github, gitlab, etc. to another one.

## Requirements

* Python 2.x or 3.x
* Modules: yaml, requests, git, tempfile

Run `sudo pip install pyyaml requests gitpython backports-tempfile` for python 2.x or `sudo pip install pyyaml requests gitpython` for python 3.x

## Configuration

Copy `config.yaml.template` to `config.yaml` and configure it as follows:

* `source`: A dict describing source resource (from which to clone all repos).
* `target`: The same for target resource (where to push these repos).
* `ignore`: A list of names of repositories to ignore.

A repository will be cloned and pushed only if it exists both at source and target resources, and is not listed in `ignore`.
Any other case will be specifically noted before the clone-push process.

Every dict (`source` and `target`) consists of three values:

* `api_url`: resource's API endpoint providing JSON list of repositories existing
* `name_key`: a name of the JSON key containing repository name
* `ssh_key`: a name of the JSON key containing SSH remote path

Note: for now, this tool does not support pagination. If you have, e.g. more than 100 repos on resource, while it can't provide more in one JSON page, this tool can't help much. Anyway, feel free to send a PR if you implement it in such a case.

## Install

Copy `multi-git-sync` to desired location.

## Running

Be sure you have SSH access to both of source and target resources: upload your public key to both of them, and check your private key is accessible to local SSH client.

Note: actually, you can fill `ssh_key` with a name of the JSON key containing, e.g., HTTPS remote path, but you should then enter your password/token for EACH pushed repository. Do you really want that?

Run from directory containing desired `config.yaml`.