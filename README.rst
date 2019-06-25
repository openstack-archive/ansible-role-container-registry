ansible-role-container-registry
===============================

A role to deploy a container registry.
For now, the role only support Docker Registry v2.


Role Variables
--------------

.. list-table:: Variables used for container registry
   :widths: auto
   :header-rows: 1

   * - Name
     - Default Value
     - Description
   * - `container_registry_debug`
     - `false`
     - Enable debug option in Docker
   * - `container_registry_deploy_docker`
     - `true`
     - Whether or not to deploy Docker
   * - `container_registry_deploy_docker_distribution`
     - `true`
     - Whether or not to deploy Docker Distribution
   * - `container_registry_deployment_user`
     - `centos`
     - User which needs to manage containers
   * - `container_registry_docker_options`
     - `--log-driver=journald --signature-verification=false --iptables=false --live-restore`
     - Options given to Docker configuration
   * - `container_registry_insecure_registries`
     - `[]`
     - Array of insecure registries
   * - `container_registry_network_options`
     - `[undefined]`
     - Docker networking options
   * - `container_registry_host`
     - `localhost`
     - Docker registry host
   * - `container_registry_port`
     - `8787`
     - Docker registry port
   * - `container_registry_mirror`
     - `[undefined]`
     - Docker registry mirror
   * - `container_registry_storage_options`
     - `-s overlay2`
     - Docker storage options
   * - `container_registry_selinux`
     - `false`
     - Whether or not SElinux is enabled for containers
   * - `container_registry_additional_sockets`
     - `[undefined]`
     - Additional sockets for containers
   * - `container_registry_skip_reconfiguration`
     - `false`
     - Do not perform container registry reconfiguration if it's already configured
   * - `container_registry_logins`
     - `[]`
     - A dictionary containing registries and a username and a password associated with the registry.
       Example: {'docker.io': {'myusername': 'mypassword'}, 'registry.example.com:8787': {'otheruser': 'otherpass'}}

Requirements
------------

 - ansible >= 2.4
 - python >= 2.6

Dependencies
------------

None

Example Playbooks
-----------------

Modify Image
~~~~~~~~~~~~

The following playbook will deploy a Docker registry:

.. code-block::

    - hosts: localhost
      become: true
      roles:
        - container-registry

License
-------

Apache 2.0
