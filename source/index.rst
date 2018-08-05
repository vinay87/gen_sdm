
============================================================
The Archimedes Simulation Data & Process Management System
============================================================

`Archimedes` is a `Simulation Process & Data Management System` developed at the GKN Driveline GEN Team, that is 
targetted towards core-engineering processes which integrate `Computer Aided Analysis` or 
`Computer Aided Engineering`. Any process that involves `CAE` can benefit from these services and tools.

The goal of the SDM is to craft a service that is, by core definition, easy to use and integrate. Ease of use is paramount in an environment that has
people of varying temperments and experience. In fact, at first glance, the SDM should be so easy to use that to do their work otherwise should seem
counter-intuitive and time-consuming.

-------------------------
Components of Archimedes
-------------------------

`Archimedes` comes with several use cases in mind, and thus integrates several components tailored for different sorts of users.

1. `James Watt` : The SDM Interface

    `James Watt`: is a UI that serves as a primary point of contact for all the engineers using these services. It consists of a Web Interface,
    a desktop client that integrates the web interface, a mobile interface commandline tools, a python library and a general purpose HTTP API
    so that it may be integrated into any application, even vendor supplied ones.

    Example use cases::

        * [Easy] Submission of jobs via selected work instruction through web/desktop client.
        * [Easy] Getting notifications for running/completed jobs via desktop client.
        * [Intermediate] Submission of runs via Marc.
        * [Intermediate] Checking jobs via Zulip/Telegram bots
        * [Advanced] Submission of jobs via MS Excel
        * [Advanced] Powershell scripts to submit runs.
        * [Advanced] Custom python scripts to perform preprocessing for adhoc jobs without a detailed work instruction 
    
    `James Watt` allows the following features::

        * Submission of Runs (Via `Ramanujan`)
        * Search UI (via Elastic Search)
        * Project Creation / Management (via Redmine)
        * Visualization (via Grafana, D3.js and Python)

2. `Ramanujan` : The Solver Services 

    `Ramanujan` comprises the background services that control the actual queuing and execution of tasks. It integrates a `Directed Acyclic Graph` 
    philosophy to the job execution, ensuring that **every** portion of the job executed is recorded via a database. `Ramanujan` can allow users to 
    design complicted work instructions, *vis a vis* "Ways of Working (WoWs)" that can branch off into separate machines. Jobs can be resumed, partially extracted or 
    even share inputs between one another. The internal workings of `Ramanujan` integrate a series of message queues using the Publisher-Subscriber model, 
    a series of worker services that are configured to launch on the cluster-nodes, and a series of plugins for the solvers, such as Mentat, Particle Works, OptiStruct etc.
    
    Deployment via `Ramanjan` is via Ansible, using the package to start services on configured machines. These machines can be tagged for a few critical parameters such as ::

        * Operating System
            + Windows Solver Services (With & Without GPU)
            + Linux Solver Services (With & Without GPU)
        * GPU Availability
            + NVidia
            + AMD
            + None
    
    Another feature of `Ramanujan` is a wrapper for the GPUs, to detect and control which GPU the program must be executed on. The clients can also be configured to limit job memory and CPU 
    availability via Linux `CGROUPS` or some similar means.

3. `Diesel` : The Data Management Services (SVN Linker / SVN scripts / crons)

    `Diesel` is the fuel of `Archimedes`. It provides the services for data management. It orchestrates how data is managed, how it is moved or cloned between sites. It can be configured 
    to orchestrate the movement of data between repositories, or between physical sites or machines.

    Some of the features are::

        * Automatic recording of job inputs into Subversion.
        * Subversion hooks
        * Creation of SVN Repositories
        * Mapping of directories to tasks in Redmine
        * Creation of proper folder structure in SVN, management of the movement between repositories.
4. `Peter` : The Authentication Services (authentication api)

        `Peter` is the authentication service. It controls the tokenization and verification of said tokens.

        It should allow one to easily plugin any sort of auth services so that `Archimedes` doesn't need an additional login ID.

5. `DaVinci` : Product Data Management (PDM) Connection Services
    
    `DaVinci` is a series of connectors to various PDM services such as Team Center and Windchill. 

6. `Nikola` : Data Analysis Services

    `Nikola` provides the data mining and data analysis services so that the data is available for Engineers to thoroughly understand. 
    It will also provide an API that sits on top of TensorFlow and PyTorch for data science using the processed data.

7. `Imhotep` : Search & Indexing Services

    `Imhotep` integrates the search and indexing services by providing parsers for every possible file format. It integrates easily into the DAGs so that once a job is complete, it can 
    be indexed and ready for search.

-----------
Tech Stack
-----------

1. Databases:
    * MySQL (migrate to Postgres)
    * ZODB (Microservice internal)
2. Service Registry
    * Consul
3. Message Queue
    * RabbitMQ
4. UI
    * Vue.js
    * Bulma
    * Electron
    * Command Line Interface
    * Plugins in Python 2.5/2.7/3.x, TCL/TK, and VBA
    * Cordova for Mobile
    * Apache Guacamole (For remote display)
5. API
    * Python 3/Flask
    * Swagger
    * Socket.io
6. Deployment & Provisioning
    * Docker
    * Vagrant
    * Oracle VirtualBox
7. Visualization
    * Grafana
    * Python: Matplotlib, Bokeh
    * Javascript: D3.js
8. Event-Based DAGs
    * Airflow with inhouse plugins
9. Developer Tools
    * Subversion (for Engineering files)
    * git (for software)
    * Gitlab (For developer coordination)
    * Travis CI (For automated testing)
    * Logstash
    * Kibana
    * Portainer
    * Grafana
    * Jupyter