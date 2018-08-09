==========================
Archimedes Infrastructure
==========================

.. note::

  Several nodes of the archimedes system are on VMs, on a vSphere virtualization server.
  As of now, we are allowed to provision 49 VMs, with the following IP range.

  Names:   dllohsr250 - dllohsr299
  IPs:    10.143.1.190 - 10.143.1.239    Netmask: 255.255.255.0   Default Gateway: 10.143.1.254

Components (some will be shared on 1 VM):

1. loadbalancer
#. GitLab
#. Travis CI
#. Portainer
#. Ansible Server
#. Postgres DB
#. airflow | mara | luigi server
#. grafana server
#. zulip server
#. readthedocs server

-----------
dllohsr250
-----------

.. note::

  IP : 10.143.1.190
  long-url : dllohsr250.driveline.gkn.com
  hostname: dllohsr250
  human url cae.driveline.gkn.com

Services:

- (loadbalance) haproxy | nginx

-------------
dllohsr251
-------------

.. note::

  IP : 10.143.1.191
  long-url : dllohsr251.driveline.gkn.com
  hostname: dllohsr251
  human url cae-gitlab.driveline.gkn.com

Services:
- (source control) gitlab

-----------
dllohsr252
-----------

.. note::

  IP : 10.143.1.192
  long-url : dllohsr252.driveline.gkn.com
  hostname: dllohsr252
  human url: cae.driveline.gkn.com/loadbalancer

Services:
- (source control) gitlab

