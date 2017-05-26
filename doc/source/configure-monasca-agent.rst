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

Setting up monasca-agent
~~~~~~~~~~~~~~~~~~~~~~~~

The monasca-agent playbook targets all hosts and containers. In that
way, to install monasca-agent no configuration is necessary, simply
build the monasca-agent packages/virtual environmnet (if not built
already) and run its playbook:

   .. code-block:: console

       # cd /opt/openstack-ansible/playbooks
       # openstack-ansible repo-build.yml
       # openstack-ansible os-monasca-agent-install.yml

Plugins
~~~~~~~

By default the monasca-agent role configures the following plugins:

   - apache
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

Dashboards
~~~~~~~~~~

Sample grafana dashboards for visualization of some metrics collected
by the configured plugins are also available at the
`monasca-agent role repository`_.

.. _monasca-agent role repository: https://github.com/openstack/openstack-ansible-os_monasca-agent/tree/master/dashboards
