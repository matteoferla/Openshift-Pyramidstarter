# Pyramidstarter README

## App.py
There are many ways to get your pyramid project running on Openshift.  This is one example.  I use Waitress as the server —for others see `app.py`.    
The Openshift 3 entrypoint is `app.py`. `wsgi.py` is no longer an option.   
There are two ini files, `production.ini` is the "normal" version. `development.ini` is strictly for development and will give you access to the python console to inspect errors. the choice of the two is in `app.py`, where the latter is run only on localhost.

## Note about Openshift version 3
This is a mod of [Fatfantasma's Openshift-Pyramidstarter](https://github.com/fatfantasma/Openshift-Pyramidstarter).     

## Requirements
To import a given package that is not part of the core, add it to the list in `requirements.txt`.    
Cheat: to copy a given python installation `pip freeze > requirements.txt`.     
Pip in the Openshift 3 starter is version 7, not 9.
To update to the latest in Openshift when configuring the build add the variable `UPGRADE_PIP_TO_LATEST=true`. This is required if you want numpy and scipy which are installed by wheel in the latter version.     
In Openshift Starter the newest RHEL python image (formerly "catridge") is 3.5. This runs both `requirements.txt` and `setup.py`.
However, in never versions (_e.g._ CentOS 3.6 used in the `Dockerfile` or in Openshift for rich people) the latter is not.
To make `setup.py` run there add a dot in the requirement list (_i.e._ install this, as a `setup.py` is afterall how pip installs stuff)—
pip installs packages based on what requires what, but in case of neutrality it runs the bottom ones first, so add it to the top.    
Also there is the possibility that the memory needed to build is insufficient as happens in version 2 for pandas (which was never meant for Python 3.2), so up the memory.     
In the previous version the environment was determined with `os.environ`, the variables have changed. If you care to know what they are just print them.

NB. The Dockerfile is not needed, but everyone loves Docker and is there just in case.

## Route
The default route is 8080, but this can be changed in the Openshift console by adding a new route. NB. this will give you a different URL.