===========================================================
Configuring the Monitoring (monasca) agent (optional)
===========================================================

.. note::

   This feature is experimental at this time and it has not been fully
   production tested yet.

The Monasca Agent is a modern Python monitoring agent for gathering
metrics and sending them to the Monasca API. The Agent supports
collecting metrics from a variety of sources.

The Agent is extensible through configuration of additional check
and setup plugins, written in Python.

Configuring target hosts
~~~~~~~~~~~~~~~~~~~~~~~~

Modify ``/etc/openstack_deploy/conf.d/monasca.yml`` by adding a list of
``monasca-agent-infra_hosts``, containing all the hosts that needs to
be monitored:

In ``monasca.yml``:

   .. code-block:: yaml

       [...]

       monasca-agent-infra_hosts:
         infra01:
           ip: INFRA01_IP_ADDRESS
         infra02:
           ip: INFRA02_IP_ADDRESS
         infra03:
           ip: INFRA03_IP_ADDRESS


Replace ``*_IP_ADDRESS`` with the IP address of the br-mgmt container
management bridge on each target host.

Setting up monasca-agent
~~~~~~~~~~~~~~~~~~~~~~~~

Build the monasca-agent packages/virtual environment (if not
built already) and run its playbook:

   .. code-block:: console

       # cd /opt/openstack-ansible/playbooks
       # openstack-ansible repo-build.yml
       # openstack-ansible os-monasca-agent-install.yml

Plugins
~~~~~~~

By default the monasca-agent role configures the following plugins:

   - apache
   - ceph
   - cpu
   - crash
   - disk
   - haproxy
   - host_alive
   - http_check
   - kafka_consumer
   - libvirt
   - load
   - mcache
   - memory
   - mysql
   - network
   - ntp
   - postfix
   - process
   - rabbitmq
   - supervisord
   - zk

More information about the available plugins, its configuration
and metric details is available at the `monasca-agent repository`_.

.. _monasca-agent repository: https://github.com/openstack/monasca-agent/blob/master/docs/Plugins.md
