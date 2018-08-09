.. intro to archimedes

------------------------------------
Introduction: Why ``Archimedes``?
------------------------------------

Mechanical Engineering companies deal with a large volume of data. However, compared to retail, this
data is fundamentally different. If one were to create an analogy between a retail company where one
set of data could be everything related to a "sale", an Engineering company's data is usually never
similar in volume by number. Instead, one set of data is usually related to a customer request, which
could be a standard or adhoc request for numerical analysis on a component. This data set could be anywhere
between 1 GB to 10 TB in filesize, and there could be a few thousand such tasks every year.

Conventional methodology at Engineering companies is mostly manual when it comes to the analysis
process. Most companies follow standard processes, standard in the sense that they define. However, it is
easily observed that there is a technological gap between the processes at an Engineering company when it
comes to data management when compared to an e-retail company.

Consider this situation for example:

.. blockdiag::
    :caption: Typical Analysis Scenario

    blockdiag admin {
      default_fontsize = 10;
      span_width=30;
      span_height=35;
      default_node_color = "#c2c2c2";
      customer [numbered = 1, label = "Customer Input", color="white", textcolor="black"]
      cae [numbered = 3, label = "Computer Aided\nEngineering", color="skyblue", width=160];
      engg [numbered = 2, label = "Engineers", color="yellow"];
      srv [label = "Servers"];
      lclmc [label = "Local Machines"];
      data [numbered = 4, label = "Engineering Data", color= "red", textcolor = "white", fontsize = 14, width= 150, height=40, style=dotted];
      search [label = "Search Engine"];
      wows [label = "Work Instructions"];
      svn [label = "Version Control"];
      doe [label = "Design of Experiments\nMachine Learning", height=60];

      reports [numbered = 5, label = "Reports", color="skyblue"];
      licenses [label = "licenses", width=64];

      customer -> engg [color="blue"];
      engg -> wows;
      data -> wows [style="dotted"];
      wows -> cae [color="blue", thick];
      engg -> cae [color="blue", thick];
      cae -> lclmc [color="blue", thick];
      cae -> srv [color="blue", thick];
      srv -> data [color="blue", thick];
      lclmc -> data [color="blue", thick];
      licenses -> cae;
      data -> search;
      data -> svn;
      data -> doe;
      doe -> cae;
      data -> reports [color="blue", thick];
    }

Such a scenario would be difficult to set up in an environment which has several different varieties of
computers, servers and users. It is such, not for lack of tries. Most certainly not. Companies have constantly
put their efforts into setting up such a system, and they have come to some manner of success over the years.
Some companies choose to use readymade solutions, and there are caveats therein.


Version control, automated testing, deployment or containerization isn't usually found at mechanical
engineering companies. It is not for lack of knowledge, but mostly because engineering companies aren't
*usually* focussed on their software. They're focussed in delivering a product that doesn't fail.

This demands an analysis, or simulation process & data management system that is robust. Many CAE and CAD software
vendors are coming up with solutions, but most of them are still not widely used. The industry is plagued with
closed-source or limited-support principles, and this causes the customer to usually stop using the tools because
support is slow, or even the smallest request is usually never free. In addition, the software vendors usually
come up with certain requirements that cannot easily be met, either related to hardware or software.
Their deployment is often difficult. To add to the problem, most engineering companies are paranoid about accepting
open source technologies, concerned about the long term support and sustenance.

``Archimedes`` hopes to solve that purpose. It is a `Simulation Process Data Management System` that will
scale horizontally, that will be easy to use, and can be plugged into **any** pre-existing situation.
It is designed to be deployable with ease, intuitive to use, and can be used on any platform.

``Archimedes`` is designed so that if a component must be replaced, so be it, but it should not affect the rest
of the system. It acknowledges that this industry is used to slow change, and brings in an idealogy that is
designed around having a robust communication methodology between the old and the new.

The way we manage this is through microservices, dedicated to keeping ``Archimedes`` alive.

Simple Use Case Example
------------------------

A customer (internal or external), comes to an Analysis engineer and asks him/her to perform a type of analysis. The engineer
then has to prepare the input statement in a format that is acceptible to the software he/she is dealing with and then submit
said input files to the solver. The solver returns to the user with the results, which he/she then must prepare in a format
that the customer will appreciate. The customer may come back with a query, and the engineer must resolve said query in time.

In simpler terms:

.. actdiag::
      :caption: Analysis Flow for Scenario #1

      actdiag analysis {
        node_width=150

        input -> receive -> preprocessing -> run -> postprocessing -> report
        report -> acknowledge -> query -> correction -> closure

        lane customer {
          label = "Customer";
          input [label ="Create Request"];
          acknowledge [label = "Receive Report"];
          query [label = "Raise Question"]
          closure [label = "Accept Solution"];
        }

        lane engineer {
          label = "Engineer"
          receive [label = "Analyse Request\nStatement"];
          preprocessing [label = "Preprocess\nInput Files"];
          postprocessing [label = "Postprocess\nOutput Data"];
          report [label = "Prepare Report\nFile"];
          correction [label = "Resolve\nQueries"];
        }
        lane cluster {
          label = "CAE System"
          run [label = "Run Solvers on Local\nMachine or Server",height=60]
        }
      }

Assume for a moment that the customer is satisfied with this solution, and doesn't ask for any thing else.
With such a simple request, it is not uncommon to already deal with 1TB of data. This is usual for the scenario, in fact.

Now, add a complexity to this problem statement. Assume that the customer came back with some information, realizing that the report given
by the engineer is insufficient because of the lack of data. Now, the engineer must adjust his/her inputs, and redo the analysis. This
adds to the problem. The additional data could be something simple in that the customer did not explain how the component was being
really used in the field. Or it could be that the customer said that the material was going to be changed. It could also be that the customer
changed the loading pattern and asked for the engineer to rerun the analysis.

.. actdiag::
      :caption: Analysis Flow for Scenario #2

      actdiag analysis {
        node_width=150

        input -> receive -> preprocessing
        preprocessing -> run -> postprocessing -> report 
        report -> acknowledge -> query -> correction
        correction -> input_2 -> receive_2
        receive_2 -> preprocessing_2 -> run_2
        run_2 -> postprocessing_2 -> report_2 -> closure

        lane customer {
          label = "Customer";
          input [label ="Create Request"];
          input_2 [label ="Add additional data"];
          acknowledge [label = "Receive Report"];
          closure [label = "Accept Solution"];
        }

        lane engineer {
          label = "Engineer"
          receive [label = "Analyse Request\nStatement"];
          receive_2 [label = "Add New Data\nTo Request Statement"];
          preprocessing [label = "Preprocess\nInput Files"];
          preprocessing_2 [label = "Preprocess\nInput Files"];
          postprocessing [label = "Postprocess\nOutput Data"];
          postprocessing_2 [label = "Postprocess\nOutput Data"];
          correction [label = "Resolve\nQueries"];
          report [label = "Prepare Report\nFile"];
          report_2 [label = "Prepare New Report\nFile"];
        }
        lane cluster {
          label = "CAE System"
          run [label = "Run Solvers on Local\nMachine or Server",height=60]
          run_2 [label = "Run Solvers on Local\nMachine or Server",height=60]
        }
      }

Imagine, for an instant, that the customer's request is something that is pretty standard and common. How are we to record this? 

With a system of practise that is at once archaic and inflexible, recording activity that is constantly 
changing is infeasible. Think about it for a moment: *you have a system that hates change, and you want to induce 
and monitor change therein!* However, this scenario **is** standard practise for the industry.

Many vendor-provided SPDM solutions seek to solve this problem, however, they are oftentimes developed for a very generic usecase,
and the vendor assumes that the company would be willing to change their data center setup to suit their software development decisions.

This is the major caveat of existing SPDM systems. Asking companies to greatly change their ways of working to suit their design is a 
fallacy. No company would be willing to. If it did, it would require extreme discipline and unnerving courage.

``Archimedes`` hopes to bring in **existing** ways of working into its fold. Does half your team use Jira for problem tracking 
while the other half uses MS Excel? Then ``Archimedes`` can be used. Do your engineers prefer Windows machines and is asking them to
learn ``qsub`` or ``qstat`` an additional burden? Then ``Archimedes`` is for you.

``Archimedes`` is for everyone who hopes to improve their analysis process and get a plethora of benefits, not through drastic change, but through
subtle yet robust change.

This section of the documentation is largely a pitch, to help new users understand why they'd need ``Archimedes``, and how it can help them.

.. toctree::
    :caption: More About Archimedes

    microservices
    components
    deployment
