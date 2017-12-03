===============================
OpenStack-Ansible Monasca-Agent
===============================

.. toctree::
   :maxdepth: 2

   configure-monasca-agent.rst

Ansible role for deploying Monasca Monitoring-as-a-Service agent.

This role installs the following Systemd services:

    * monasca-agent

To clone or view the source code for this repository, visit the role repository
for `os_monasca-agent <https://github.com/openstack/openstack-ansible-os_monasca-agent>`_.

Default variables
~~~~~~~~~~~~~~~~~

.. literalinclude:: ../../defaults/main.yml
  :language: yaml
  :start-after: under the License.

Dependencies
~~~~~~~~~~~~

This role needs pip >= 7.1 installed on the target host.

Example playbook
~~~~~~~~~~~~~~~~

.. literalinclude:: ../../examples/playbook.yml
  :language: yaml

Tags
~~~~

This role supports the following tags:

    * ``monasca-agent-install``: used to install and upgrade monasca-agent;
    * ``monasca-agent-config``: used to manage monasca-agent configuration;
