# Dispatcher for early adopters

### To install:

setup your python virtualenv:

    [ setup virtual env ], follow steps here: https://confluence.oceanobservatories.org/display/CIDev/New+developer+tutorial
    mkvirtualenv dispatcher

clone and configure:

    git clone git://github.com/ooici-eoi/dispatcher_deployment.git 
    cd dispatcher_deployment

    python bootstrap.py
    ./bin/buildout dispatcher-config:host=<your host here> dispatcher-config:sysname=<your sysname here>



### To run:

#### via supervisord

    ./bin/dispatcher-supervisord

Now you can navigate to http://localhost:9001 to see it running, login with ooici/sekrit

#### running "interactively" (no CC shell)

    ./bin/dispatcher

#### running via CC (debugging only)

    ./bin/twistd -n cc -h <your host here> -a sysname=<your sysname here> res/apps/dispatcher.app


