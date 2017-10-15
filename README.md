# Pyramidstarter README

## Note about Openshift version 3
This is a mod of [Fatfantasma's Openshift-Pyramidstarter](https://github.com/fatfantasma/Openshift-Pyramidstarter).    
The Openshift 3 entrypoint is `app.py`. `wsgi.py` is no longer an option.    
Pip in the Openshift 3 starter is version 7, not 9.
To update to the latest in Openshift when configuring the build add the variable `UPGRADE_PIP_TO_LATEST=true`. This is required if you want numpy and scipy which are installed by wheel in the latter version.     
In Openshift Starter the newest RHEL python image (formerly "catridge") is 3.5. This runs both `requirements.txt` and `setup.py`.
However, in never versions (_e.g._ CentOS 3.6 used in the `Dockerfile` or in Openshift for rich people) the latter is not.
To make `setup.py` run there add a dot in the requirement list (_i.e._ install this, as a `setup.py` is afterall how pip installs stuff)—
pip installs packages based on what requires what, but in case of neutrality it runs the bottom ones first, so add it to the top.    
Also there is the possibility that the memory needed to build is insufficient as happens in version 2 for pandas (which was never meant for Python 3.2), so up the memory.     
In the previous version the environment was determined with `os.environ`, the variables have changed. If you care to know what they are just print them.

NB. The Dockerfile is not needed, but everyone loves Docker and is there just in case.

## About this Starter
There are many ways to get your pyramid project running on Openshift.  This is one example.  I use Waitress as the server.  The demo code currently is setup using wsgi simple server.  You can comment/uncomment out the code in app.py as you like and select what server you want to use.

Openshift uses two different entry points for starting your app.  These are 'app.py' and 'wsgi.py'.  Only use one.

Use 'app.py' to start your own server such as waitress, cherrypy, etc.

Use 'wsgi.py' to just use Openshift's Apache server.

Rename/delete these files accordingly to enable or disable depending on what you want to do.


Add the packages you want to be installed in the setup.py