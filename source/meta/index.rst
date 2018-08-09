.. intro to archimedes

--------------------------------
Introduction: Why ``Archimedes``?
--------------------------------

Mechanical Engineering companies deal with a large volume of data. However, compared to retail, this data is fundamentally different. If one were to create
an analogy between a retail company where one set of data could be everything related to a "sale", an Engineering company's data is usually never similar in 
volume by number. Instead, one set of data is usually related to a customer request, which could be a standard or adhoc request for numerical analysis on a
component. This data set could be anywhere between 1 GB to 10 TB in filesize, and there could be a few thousand such tasks every year.

Conventional methodology at Engineering companies is mostly manual when it comes to the analysis process. Most companies follow standard processes, standard in the
sense that they define. However, it is easily observed that there is a technological gap between the processes at an Engineering company when it comes to data management
when compared to an e-retail company.

Version control, automated testing, deployment or containerization isn't usually found at mechanical engineering companies. It is not for lack of knowledge, but mostly because
Engineering companies aren't focussed on their software. They're focussed in delivering a product that doesn't fail.

This demands an analysis, or simulation data management system that is robust. Many software vendors are coming up with solutions, but most of them are still not widely used. The industry
is plagued with closed-source or limited-support principles, and this causes the customer to usually stop using the tools because support is slow, or even the smallest request is usually
never free. In addition, the software vendors usually come up with certain requirements that cannot easily be met, either related to hardware or software. Their deployment is often difficult.

``Archimedes`` hopes to solve that purpose. It is a `Simulation Process Data Management System` that will scale horizontally, that will be easy to use, and can be plugged into **any**
pre-existing situation. It is designed to be deployable with ease, intuitive to use, and can be used on any platform.

The way we manage this is through microservices, dedicated to keeping ``Archimedes`` alive.

.. toctree:: 
    :caption: More About Archimedes

    components
    deployment
