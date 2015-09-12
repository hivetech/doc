---
sidebar_current: "dna"
---

# DNA

> Hacking environment genetics

> By [Hive Tech](http://unide.co)


DNA is a community-driven compilation of dotfiles and projects, aimed
at creating the most awesome and powerful development environment.
We use it here at Hivetech to setup fresh new machines and provide our
[hivelab charm](https://github.com/hivetech/cells/tree/master/precise/hivelab)
for the Unide project.

Installation is performed through famous configuration managers like ansible
and [salt](http://saltstack.com/community.html) (currently focused on [ansible](www.ansibleworks.com)) as they obviously play nicely with a
dotfiles repository and allow you to configure in seconds thousands of machines,
as well as simply your beloved local one.

It is designed to be plugin-friendly: A new awesome, github featured
project you discovered for your environment ? Star it and just plug
a playbook ( / minion / recipe / manifest / script) in the plugin directory.

If you are familiar with [docker](http://www.docker.io), you can test the
environment:

```console
$ docker pull hivetech/lab
$ ID=$(docker run -d hivetech/lab)
$ PORT=$(docker port $ID 22)
$ ssh prototype@127.0.0.1 -p $PORT   # Password: proto
```


Content
-------

This is heavy work in progress. Right now I'm cleaning and moving here my
previous repo (https://github.com/hackliff/Dotfiles)

* Shell

    * Oh-my-zsh - [A community-driven framework for managing your zsh configuration](https://github.com/robbyrussell/oh-my-zsh)
    * Oh-my-fish - [Framework for managing your fish shell configuration inspired by Oh My ZSH](https://github.com/bpinto/oh-my-fish)
    * Fish-shell - [The user-friendly command line shell](https://github.com/fish-shell/fish-shell)
    * Liquidprompt - [A full-featured & carefully designed adaptive prompt for Bash & Zsh](https://github.com/nojhan/liquidprompt)
    * Bash-it - [A community bash framework](https://github.com/revans/bash-it)
    * Stderred - [Stderr output in red](https://github.com/sickill/stderred)
    * Cheat - [cheat allows you to create and view interactive cheatsheets on
      the command-line. It was designed to help remind *nix system
      administrators of options for commands that they use frequently, but not
      frequently enough to remember.](https://github.com/chrisallenlane/cheat)
    * An easy way to extend the configuration with hooks shell/customrc.sh and shell/custom-alias.sh
    * Carefully designed and organized \*rc files, screen and tmux configurations
    * [Fish shell like syntax highlighting for Zsh](https://github.com/zsh-users/zsh-syntax-highlighting)
    * [ZSH port of Fish shell's history search feature](https://github.com/zsh-users/zsh-history-substring-search)

* Versioning

    * Git flow - [Git extensions to provide high-level repository operations for Vincent Driessen's branching model](https://github.com/nvie/gitflow)
    * Gitignore.io - [Generate useful .gitignore files for your project](https://github.com/joeblau/gitignore.io)
    * Git-extras - [GIT utilities -- repo summary, repl, changelog population, author commit percentages and more](https://github.com/visionmedia/git-extras)
    * Scm breeze - [Adds numbered shortcuts to the output git status, and much more](https://github.com/ndbroadbent/scm_breeze)
    * Octogit - [giving git more tentacles](http://myusuf3.github.com/octogit/)
    * Git-hub - [Do GitHub operations from the `git` command](https://github.com/ingydotnet/git-hub)

* Dev

    * Optparse - [A BASH wrapper for getopts, for simple command line arguments](https://github.com/nk412/optparse)
    * Autopep8 - [A tool that automatically formats Python code to conform to the PEP 8 style guide](https://github.com/hhatto/autopep8)
    * Virtual Burrito - [One command to have a working virtualenv + virtualenvwrapper environment](https://github.com/brainsik/virtualenv-burrito)
    * Gvm - [Go Version Manager](https://github.com/moovweb/gvm)
    * Pyenv - [Simple Python version management](https://github.com/yyuu/pyenv), 
      with [pip-rehash](https://github.com/yyuu/pyenv-pip-rehash), [doctor](https://github.com/yyuu/pyenv-doctor),
      [installer](https://github.com/yyuu/pyenv-installer), [pip-migrate](https://github.com/yyuu/pyenv-pip-migrate), 
      [update](https://github.com/yyuu/pyenv-update) and [virtualenvs](https://github.com/yyuu/pyenv-virtualenv) plugins
    * Funcy - [A fancy and practical functional tools](https://github.com/Suor/funcy)
    * Nvm - [Node Version Manager - Simple bash script to manage multiple active node.js versions](https://github.com/creationix/nvm)
    * Pip-tools - [A set of tools to keep your pinned Python dependencies fresh](https://github.com/nvie/pip-tools)
    * Tox - [standardize testing in python](http://tox.readthedocs.org/en/latest/)
    * Rbenv - [Groom your app’s Ruby environment](https://github.com/sstephenson/rbenv)
    * Ruby-build - [Compile and install Ruby](https://github.com/sstephenson/ruby-build)
    * Rbenv-bundler - [an rbenv plugin that makes shims aware of bundle installation paths](https://github.com/carsomyr/rbenv-bundler)
    * Rbenv-gemset - [Add excellent gem / gemset management to your rbenv!](https://github.com/jf/rbenv-gemset)
    * Rubocop - [A robust Ruby code analyzer, based on the community Ruby style guide](https://github.com/bbatsov/rubocop)
    * Gocode - [An autocompletion daemon for the Go programming language](https://github.com/nsf/gocode)
    * Simple Defects - [SD is a peer-to-peer bug tracker that’s built for sharing and use both online and offline](http://syncwith.us/sd/)

* Plugins

    * z - [z is the new j, yo](https://github.com/rupa/z)
    * t - [A command-line todo list manager for people that want to finish tasks, not organize them](http://stevelosh.com/projects/t/)
    * Bd - [Quickly go back to a parent directory in linux](https://github.com/vigneshwaranr/bd)
    * Httpie - [HTTPie is a CLI, cURL-like tool for humans](https://github.com/jkbr/httpie)
    * Dropbox - [A BASH script which can be used to upload, download, list or delete files from Dropbox](https://github.com/andreafabrizi/Dropbox-Uploader)
    * View-doc - Use [DocumentUp](https://github.com/jeromegn/DocumentUp) and [Daux.io](https://github.com/justinwalsh/daux.io) to browse your project doc
    * Autoenv - [Directory-based environments](https://github.com/kennethreitz/autoenv)
    * LaTex - [A document preparation system](http://www.latex-project.org/)
    * jq - [Command-line JSON processor](http://stedolan.github.io/jq/)
    * Pyhn - [Hacker news in your terminal](https://github.com/socketubs/pyhn)
    * Howdoi - [Instant coding answers via the command line](https://github.com/gleitz/howdoi)

* [Vim](https://github.com/hivetech/dna/tree/master/vim/readme.markdown#plugins)

* [Python](https://github.com/hivetech/dna/tree/master/python/README.md)

* [Utils](https://github.com/hivetech/dna/tree/master/utils/readme.markdown)

* [Openbox](https://github.com/hivetech/dna/tree/master/openbox/readme.markdown)

Usage (ansible style)
-----

```console
$ export DNA_PATH=where/you/want/dna  # Optional, default will be /opt/dna
$ export EDITOR=nano                  # Optional, default will be vim

$ wget -qO- https://raw.github.com/hivetech/dna/master/bootstrap.sh | bash

$ cd $DNA_PATH && rake -T
$ rake dna:synthetize               # Default will setup your local machine

$ # Once installed
$ cheat lab
$ cheat <sub-command>  # git-extras for example
```

Notice the `synthetize` action is idempotent.


Sandbox mode (still ansible style)
------------

You can test the project in a virtualize environment. Typical use case would be
to enjoy a clean dev env while working in docker powered machines, or test your
awesome fork.

```console
$ ./synthetize --help
$ ./synthetize --action prototype --check --verbose   # Changes won't be applied, just tested
$ ./synthetize --action target --port 49500 --image hivetech/prototype --user you
$ ./synthetize connect  # Password is proto (set in dockerfile)
```

(**Experimental**) A Vagrantfile is provided and you can check out the
[documentation](http://docs.vagrantup.com/v2/provisioning/ansible.html) for
more informations. Make sure `dna/provision/ansible/data.yml` suits you and a
vagrant section is present in `dna/provision/ansible/hosts`.

You also have to modified `hosts` variable in site.yml to `vagrant` because of
a weird vagrantfile bug.

Then just run `vagrant up && vagrant ssh`.

License
-------

DNA is available under the [Apache License, Version
2.0](http://www.apache.org/licenses/LICENSE-2.0.html).

---
##### last modified on: April 29, 2014
---
