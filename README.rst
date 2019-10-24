ansible-role-container-registry
===============================

A role to deploy a container registry and provide methods to login to it.
For now, the role only support Docker Registry v2.
The login currently doesn't work with hub.docker.com.


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
   * - `container_registry_docker_disable_iptables`
     - `false`
     - Adds --iptables=false to /etc/sysconfig/docker-network config
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


Running local testing
---------------------

Local testing of this role can be done in a number of ways.

Mimic Zuul
~~~~~~~~~~

Sometimes its nessisary to setup a test that will mimic what the OpenStack gate
will do (Zuul). To run tests that minic the gate, `python-virtualenv` `git`,
`gcc`, and `ansible` are required.

.. code-block:: shell

    $ sudo yum install python-virtualenv git gcc


Once the packages are installed, create a python virtual environment.

.. code-block:: shell

    $ python -m virtualenv --system-site-packages ~/test-python
    $ ~/test-python/bin/pip install pip setuptools --upgrade


Now install the latest Ansible

.. code-block:: shell

    $ ~/test-python/bin/pip install ansible


With Ansible installed, activate the virtual environment and run the
`run-local.yml` test playbook.

.. code-block:: shell

    $ source ~/test-python/bin/activate
    (test-python) $ ansible-playbook -i 'localhost,' \
                                     -e "tripleo_src=$(realpath --relative-to="${HOME}" "$(pwd)")" \
                                     -e "ansible_user=${USER}" \
                                     -e "ansible_user_dir=${HOME}" \
                                     -e "ansible_connection=local" \
                                     zuul.d/playbooks/run-local.yml


Running Molecule directly
~~~~~~~~~~~~~~~~~~~~~~~~~

It is also possible to test this role using molecule directly. When running
tests directly it is assumed all of the dependencies are setup and ready to
run on the local workstation. When

.. code-block:: shell

    $ molecule test --all
