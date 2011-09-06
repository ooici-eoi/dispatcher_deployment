# Dispatcher for early adopters

**You must be registered with the ION system and your user must have early-adopter priviledges for the dispatcher to function.**  Contact Chris Mueller for more info.

## To install:

### VirtualEnv
setup your python virtualenv:

    [ setup virtual env ], follow steps here: https://confluence.oceanobservatories.org/display/CIDev/New+developer+tutorial
    mkvirtualenv dispatcher

### Obtain the deployment
#### With GIT:

    git clone git://github.com/ooici-eoi/dispatcher_deployment.git 
    cd dispatcher_deployment

#### Without GIT:
download tarball from https://github.com/ooici-eoi/dispatcher_deployment/archives/master
*NOTE: the 7 characters at the end of the downloaded file may differ from those below

    tar xfz ooici-eoi-dispatcher_deployment-6ca540a.tar.gz
    mv ooici-eoi-dispatcher_deployment-6ca540a dispatcher_deployment
    cd dispatcher_deployment

### Configure the deployment:
from the 'dispatcher_deployment' directory, configure the deployment with:

    python bootstrap.py
    ./bin/buildout dispatcher-config:host=<your host here> dispatcher-config:sysname=<your sysname here>

## To run:

### via supervisord:

    ./bin/dispatcher-supervisord

Now you can navigate to http://localhost:9001 to see it running, login with ooici/sekrit

### running "interactively" (no CC shell):

    ./bin/dispatcher

### running via CC (debugging only):

    ./bin/twistd -n cc -h <your host here> -a sysname=<your sysname here> res/apps/dispatcher.app

## To update:

### If installed with git:
Turn off the current dispatcher with:

    bin/dispatcher-supervisord stop
    bin/dispatcher-supervisord shutdown
    ps –ef | grep dispatcher
    kill –9 <any processes the grep finds>
    
Run the following command:

    bin/update.sh

**OR** perform the update manually (update.sh records your last buildout settings so you don't have to retype all of this):

    git pull
    ./bin/buildout dispatcher-config:host=<your host here> dispatcher-config:sysname=<your sysname here>
    
Restart the dispatcher via supervisord:

    bin/dispatcher-supervisord

### If installed without git:

Turn off the current dispatcher:

    bin/dispatcher-supervisord stop
    bin/dispatcher-supervisord shutdown
    ps –ef | grep dispatcher
    kill –9 <any processes the grep finds>

Copy/move the "dispatcher.id" and "dispatcher_users.id" files to another location:

    mv dispatcher.id ../dispatcher.id
    mv dispatcher_users.id ../dispatcher_users.id

Delete the "dispatcher_deployment" directory:

    cd ..
    rm -r dispatcher_deployment

Download and untar the new deployment from: https://github.com/ooici-eoi/dispatcher_deployment/archives/master

    tar xfz ooici-eoi-dispatcher_deployment-6ca540a.tar.gz
    mv ooici-eoi-dispatcher_deployment-6ca540a dispatcher_deployment
    cd dispatcher_deployment

Follow the steps in the "Configure the deployment" section above but DO NOT start the dispatcher

Copy/move the "dispatcher.id" and "dispatcher_users.id" files into the new "dispatcher_deployment" directory
    
    mv ../dispatcher.id dispatcher.id
    mv ../dispatcher_users.id dispatcher_users.id

Start the dispatcher:

    bin/dispatcher-supervisord


