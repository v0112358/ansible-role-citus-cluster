
Ansible Role: Citus Cluster
=========

![CI](https://github.com/v0112358/ansible-role-citus-cluster/actions/workflows/main.yml/badge.svg) ![Ansible Role](https://img.shields.io/ansible/role/d/55983) [![GitHub license](https://img.shields.io/github/license/v0112358/ansible-role-citus-cluster)](https://github.com/v0112358/ansible-role-citus-cluster/blob/master/LICENSE.md)

Install and configure Citus cluster on your system.

Todo
------------
- Support Debian/Ubuntu

Example Inventory
------------
```
[citus_cluster:children]
citus_cluster_infra

[citus_cluster_infra]
vm-dev-citus-coordinator-0  citus_role="coordinator" pg_role="primary"
vm-dev-citus-coordinator-1  citus_role="coordinator" pg_role="standby"
vm-dev-citus-monitor-0      citus_role="monitor"  pg_role="primary"
vm-dev-citus-worker-0       citus_role="worker" pg_role="primary"
vm-dev-citus-worker-1       citus_role="worker" pg_role="primary"
vm-dev-citus-worker-2       citus_role="worker" pg_role="primary"
vm-dev-citus-worker-3       citus_role="worker" pg_role="primary"
vm-dev-citus-worker-4       citus_role="worker" pg_role="primary"
vm-dev-citus-worker-5       citus_role="worker" pg_role="primary"
```
Example Playbook
------------

```
---
- name: Deploy Citus cluster
  hosts: citus_cluster
  pre_tasks:
    - name: Verify Ansible meets Citus requirements.
      assert:
        that: "ansible_version.full is version_compare('2.10.0', '>=')"
        msg: >
          "You must update Ansible to at least 2.10.0 to use this playbook"
  roles:
    - { role: citus_cluster, tags: citus_cluster }
```

Role Variables
--------------

These variables are set in defaults/main.yml. Please review and update default password:
```
---
pg_version: 13
citus_shard_replication_factor: 1

citus_postgres_coordinator_conf_params:
  listen_addresses: "*"

citus_postgres_worker_conf_params:
  listen_addresses: "*"
 ....
```

Requirements
------------

pip packages listed in requirements.txt.

License
-------

MIT

Author Information
------------------
v0112358