
-------------------
Why Microservices?
-------------------

``Archimedes`` uses microservices to achieve its feature set. The reason this direction was selected was because of the inherent
variations in the sort of setups one can expect in an environment usually found at a Mechanical Engineering company. It is not 
usual to find users on Linux machines, capable of POSIX commands such as ``qsub`` for instance.

Using microservices, one can entirely rely on ``HTTP`` commands to communicate with a job server. HTTP is so commonplace today, and 
it has vast acceptance for its ease of use.

Using the API calls, every single feature of the ``archimedes`` server can be accessed directly from any programming language or commandline of one's
choice. A user can submit a run through an Excel macro, from a powershell script, or a TCL/TK script from within a black-box software.

This is a great advantage of the microservice idealogy and this is why it was selected for this project. In addition, if the CAE world should
ever accept mobile computing, ``Archimedes`` will be there first.

