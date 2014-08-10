Heroku buildpack: Python with SWIG
========================

SWIG install based on work done by Guy Bowden https://github.com/guybowden/heroku-buildpack-python-paybox but updated to use a more recent Python Buildpack (currently v51)

This is a [Heroku buildpack](http://devcenter.heroku.com/articles/buildpacks) for Python apps, powered by [pip](http://www.pip-installer.org/) with an additional install for SWIG which provides M2Crypto support.


Usage
-----

Example usage:

    $ ls
    Procfile  requirements.txt  runtime.txt

    $ heroku create --stack cedar --buildpack git://github.com/huxley/heroku-buildpack-SWIG-python.git

    $ git push heroku master
    ...
    -----> Fetching custom git buildpack... done
    -----> Python app detected
    -----> Fetching and installing SWIG 2
    -----> Installing ...
            SWIG installed
            updating path...
            /app/.heroku/python/bin:/app/.heroku/vendor/bin::/usr/local/bin::/tmp/codon/vendor/bin:/usr/ruby1.9.2/bin:/usr/local/bin:/usr/local/sbin:/usr/bin:/bin:/usr/sbin:/sbin:/tmp/buildpack_489c0f89-3651-40e4-b537-0659d557cb7d/vendor/bpwatch:/app/.paybox/swig/bin/
            setting SWIG_LIB environment var
    -----> Preparing Python runtime (python-2.7.8)

            ... yadda yadda ...
           
           Cleaning up...

You can also add it to upcoming builds of an existing application:

    $ heroku config:add BUILDPACK_URL=git://github.com/huxley/heroku-buildpack-SWIG-python.git

The buildpack will detect your app as Python if it has the file `requirements.txt` in the root. 

It will use Pip to install your dependencies, vendoring a copy of the Python runtime into your slug. 

Specify a Runtime
-----------------

You can also provide arbitrary releases Python with a `runtime.txt` file.

    $ cat runtime.txt
    python-3.3.2
    
Runtime options include:

- python-2.7.8
- python-3.3.2
- pypy-1.9 (experimental)
