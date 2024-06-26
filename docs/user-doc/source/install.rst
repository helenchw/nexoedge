Installation
============

Nexoedge supports installation on physical and virtual machines and container-based deployment.

For machine requirements, see :ref:`sys-requirements` for details.

Physical and Virtual Machines
+++++++++++++++++++++++++++++

Nexoedge Key Entities 
^^^^^^^^^^^^^^^^^^^^^

#. Get the Debian package (nexoedge-|version|-amd64-full.deb).
#. Update the APT repository list: 

   .. code-block:: bash

      $ sudo apt update

#. Install Nexoedge:

   .. code-block:: bash

      $ sudo dpkg -i nexoedge-<version>-amd64-full.deb && sudo apt install -f -y

   - Type 'yes' to start the systemd-managed services as needed

#. Check the status of services:

   - For the proxy,

     .. code-block:: bash

        $ sudo systemctl status ncloud-proxy

   - For the agent,

     .. code-block:: bash

        $ sudo systemctl status ncloud-agent


The package installs configuration files to ``/usr/lib/ncloud/current`` and ``/usr/lib/ncloud/sample``.
By default, proxies and agents running under the systemd-managed services use the configurations in ``/usr/lib/ncloud/current``.
For the available configuration options, see :ref:`config`.

The same procedure also applies to packages with only the proxy or agent entity, e.g., nexoedge-|version|-amd64-proxy.deb and nexoedge-|version|-amd64-agent.deb.

To uninstall the package,

- For the full package,

  .. code-block:: bash

     $ sudo apt purge -y nexoedge-full 

- For the proxy package,

  .. code-block:: bash

     $ sudo apt purge -y nexoedge-proxy

- For the agent package,

  .. code-block:: bash

     $ sudo apt purge -y nexoedge-agent


SMB/CIFS
^^^^^^^^

Unpack the release tarball, which contains

- ``scripts``: scripts to run SMB/CIFS as a service
- ``samba``: SMB/CIFS binaries with Nexoedge VFS

#. Copy the SMB/CIFS binaries to ``/usr/local``:

   .. code-block:: bash

      $ sudo cp -r samba /usr/local/

#. Set up the SMB/CIFS service

   .. code-block:: bash

      $ cd scripts
      $ sudo bash install.sh

   Enter 'yes' to start the systemd-managed service.

#. Check if the service is up

   .. code-block:: bash

      $ systemctl status ncloud-cifs

#. Create a user with password (Note: the user must already exist in the system.)

   .. code-block:: bash
      
      $ sudo /usr/local/samba/bin/pdbedit -a ncloud

#. Create the SMB/CIFS export directory

   .. code-block:: bash

      $ sudo mkdir -p /smb/ncloud
      $ sudo chmod 777 /smb/ncloud

#. Try access the SMB/CIFS share

   .. code-block:: bash

      $ sudo apt install -y smbclient
      $ smbclient -U ncloud //127.0.0.1/ncloud # Enter you password
      smb: \> ls


The SMB implementation extends Samba_ and the configuration file ``/usr/local/samba/etc/smb.conf`` can be updated according to the `Samba configuration guide`_ if needed.

To uninstall the SMB service, run the `uninstall.sh` under the `scripts` folder.

.. code-block:: bash

   $ cd scripts
   $ sudo bash uninstall.sh


Container-based Deployment
++++++++++++++++++++++++++

For container-based deployment, install the latest version of Docker engine according to `Docker official installation guide`_.


.. _Samba: https://www.samba.org/
.. _Samba configuration guide: https://www.samba.org/samba/docs/current/man-html/smb.conf.5.html
.. _Docker official installation guide: https://docs.docker.com/engine/install/

