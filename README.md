Unide Documentation
===================

Source code of [doc.unide.co](http://doc.unide.co), powered by
[middleman](http://middlemanapp.com),
[okdoc](https://github.com/hackliff/okdoc) and [docker](http://docker.io).


Generate the documentation
--------------------------

Here is how to build the doc locally.

```console
$ # Download necessary tools
$ (sudo) pip install okdoc
$ git clone https://github.com/hivetech/doc && cd doc
$ # Build the website from markdown files
$ okdoc build --to unide-doc --from .

$ # Build the middleman app
$ cd unide-doc &&\
  bundle install && \
  bundle exec middleman server

$ firefox http://localhost:4567
```

Or use docker.

```console
$ git clone https://github.com/hivetech/doc && cd doc
$ docker build --rm -t awesome/doc .
$ docker run -d --name doc -p 4567 awesome/doc
```


Licence
-------

Copyright 2014 Hive Tech S.A.S.

This documentation is available under the [MIT
License](http://opensource.org/licenses/MIT).
