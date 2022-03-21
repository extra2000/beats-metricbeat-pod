Production Deployment
=====================

Example how to deploy Metricbeat for production environment.

Clone repository
----------------

Execute the following command to clone repository:

.. code-block:: bash

    mkdir -pv ~/extra2000
    cd ~/extra2000
    git clone https://github.com/extra2000/beats-metricbeat-pod.git

Then, ``cd`` into project root directory:

.. code-block:: bash

    cd beats-metricbeat-pod

Build Metricbeat Image
----------------------

From the project root directory, ``cd`` into ``deployment/production``:

.. code-block:: bash

    cd deployment/production

Build Metricbeat image:

.. code-block:: bash

    podman build -t extra2000/elastic/metricbeat -f Dockerfile .

Deploy Metricbeat
-----------------

From the project root directory, ``cd`` into ``deployment/production``:

.. code-block:: bash

    cd deployment/production

Create config files and fix permission:

.. code-block:: bash

    cp -v configmaps/beats-metricbeat.yaml{.example,}
    cp -v configs/metricbeat.yml{.example,}
    chmod go-w configs/metricbeat.yml

Create modules:

.. code-block:: bash

    cp -v modules/beat-xpack.yml{.example,}
    cp -v modules/system.yml{.example,}
    cp -v modules/linux.yml{.example,}
    cp -v modules/elasticsearch-xpack.yml{.example,}
    cp -v modules/logstash-xpack.yml{.example,}
    cp -v modules/kibana-xpack.yml{.example,}

.. note::

    You don't need to enable all modules. Only create modules that you want to be enabled.

Create pod file:

.. code-block:: bash

    cp -v beats-metricbeat-pod.yaml{.example,}

For SELinux platform, label the following files to allow to be mounted into container:

.. code-block:: bash

    chcon -R -v -t container_file_t ./configs ./secrets modules

Load SELinux security policy:

.. code-block:: bash

    sudo semodule -i selinux/beats_metricbeat.cil /usr/share/udica/templates/{base_container.cil,net_container.cil}

Verify that the SELinux module exists:

.. code-block:: bash

    sudo semodule --list | grep -e "beats_metricbeat"

Deploy Metricbeat:

.. code-block:: bash

    podman play kube --configmap configmaps/beats-metricbeat.yaml --seccomp-profile-root ./seccomp beats-metricbeat-pod.yaml

Create systemd files to run at startup:

.. code-block:: bash

    mkdir -pv ~/.config/systemd/user
    cd ~/.config/systemd/user
    podman generate systemd --files --name beats-metricbeat-pod
    systemctl --user enable pod-beats-metricbeat-pod.service container-beats-metricbeat-pod-srv01.service
