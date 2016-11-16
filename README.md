# openstack-ansible-os_monasca-agent

# Install

### Client installation

For Mitaka and below, add ```python-monascaclient``` to the ```utility_pip_packages``` variable in  ```/opt/openstack-ansible/playbooks/utility-install.yml``` to install the monasca client in the utility hosts, and re-run the playbook.

### Add packages to repo container

Make a file ```/etc/openstack_deploy/user_variables_monasca.yml``` with the following:
```
monasca_requires_pip_packages:
  - monasca-agent
  - gevent==1.1.1
  - msgpack-python
  - netaddr
  - psutil==3.0.1
```

Then re-run the ```repo-build.yml``` playbook in the ```/opt/openstack-ansible/playbook```:

```
openstack-ansible repo-build.yml
```

### Run playbook




# Notes

### Skips repo & utility containers

By default, this skips the repo and utility containers as they do not host openstack services. Set ```skip_repo_utility_hosts``` to ```false``` to install the agent on those hosts as well.

### Generate host_alive checks

To create host_alive checks for all hosts in the Openstack-Ansible inventory,
populate host_alive_check_hosts with a list of hosts that should do the checking, ideally the monasca hosts.
```
host_alive_check_hosts:
  - monasca-1
  - monasca-2
  - monasca-3
```

To add extra hosts to the ssh host checks,
```
extra_host_alive_checks:
  - { hostname: 'test1',ip:'1.1.1.1' }
  - { hostname: 'test2',ip:'2.2.2.2' }
```

To regen the host_alive configuration after inventory changes, re-run the playbook with the tag ```regen_host_alive_checks```:
```
openstack-ansible os-monasca-agent.yml -t regen_host_alive_checks
```
# TODO

Fix process I/O access issue.

```
2016-11-14 07:16:07 UTC | DEBUG | collector | monasca_agent.collector.checks.check.process(process.py:123) | monasca-agent user does not have access to I/O counters for process 4699: <bound method Process.name of <psutil.Process(pid=4699, name='supervisord') at 140220130336016>>
```
