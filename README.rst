Hardware properties discovery for OpenStack Ironic
==================================================

.. image:: https://travis-ci.org/Divius/ironic-discoverd.svg?branch=master
    :target: https://travis-ci.org/Divius/ironic-discoverd

Running
-------

We're available on PyPI::

    pip install ironic-discoverd
    ironic-discoverd /path/to/conf

Or you can test locally::

    make test_env  # only the first time
    make test  # run tests
    .env/bin/python setup.py develop
    .env/bin/ironic-discoverd example.conf

Of course you may want to modify *example.conf* to match your OpenStack
environment.

API
---

HTTP API consist of 2 endpoints:

* ``/v1/discover`` initiate hardware discovery. Request body: JSON - list of
  UUID's of nodes to discover. All power management configuration for these nodes
  needs to be done prior to calling the endpoint.

  .. note::
      Right now this endpoint is not authenticated. It will switch to
      OpenStack authentication in the near future.

* ``/v1/continue`` intertnal endpoint for the discovery ramdisk to post back
  discovered data. Should not be used fofr anything other than implementing
  the ramdisk. Request body: JSON dictionary with keys:

  * ``cpus`` number of CPU
  * ``cpu_arch`` architecture of the CPU
  * ``memory_mb`` RAM in MiB
  * ``local_gb`` hard drive size in GiB
  * ``macs`` list of MAC addresses for all NIC's
