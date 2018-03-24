Example Twisted Klein for Azure Web App
=======================================

Base on:

* https://prmadi.com/django-app-with-httpplatformhandler-in-azure-app-services-windows/
* https://github.com/prashanthmadi/azure-django-httphandler


Azure Configuration
-------------------

It uses the Azure App Services and runs as a Web App.

In Azure Portal, go to "Deployment Options" and configure "Local Git".
Also configure an username and password for "Deployment Credentials".
This will create a dedicated Git repo for hosting the files.

From the "Development tools -> Extensions" of the Web App,
enable Python 2.7.14 32 bit.
It used Python 2.7 as for now this is the version of Twisted for which there
is a wheel on PyPI.


Azure Deployment
----------------

Each time you push to this repo, it will run the the `deploy.cmd` on the
remote server.

It uses a custom deployment script.

It uses the IIS HTTP Handler to start the Twisted Web.
For HTTP Handler configuration see:
https://docs.microsoft.com/en-us/iis/extensions/httpplatformhandler/httpplatformhandler-configuration-reference

The HTTP Handler logs on Azure as stored in D:\home\LogFiles\python.log.
You can use the "Console" from the Azure Portal and check those logs.


Local Development
-----------------

Azure will run it on Window.
For development on Linux, you can use the requirements-linux.txt file inside
a virtual environment.

From the virtualenv use this to run on port 8080::

    virtualen build
    . build/bin/activate
    pip install -r requirements-linux.txt
    python -m twisted web -p tcp:8080 --class=twistdPlugin.resource
