OpenQA
======

Role to install and bootstrap [open.qa](OpenQA) on a host

Requirements
------------

Basic `openSUSE` Linux installation with working network and `python-xml`

    zypper in python-xml

Role Variables
--------------

The following variables are set

    firewall_configure: true           # Enable firewall configuration
    firewall_interface: "public"       # Firewall interface to configure


Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: openqa, firewall_configure: true }

Post-Install steps
------------------

Checkout the [OpenQA Documentation](http://open.qa/docs/#_adding_a_new_iso_to_test) for the first steps after installing. The following is just a kick-start guide.

### Download ISOs

ISOs to be tested should be stored in `/var/lib/openqa/share/factory/iso`

    # cd /var/lib/openqa/share/factory/iso
    # wget https://download.opensuse.org/distribution/leap/15.1/iso/openSUSE-Leap-15.1-DVD-x86_64.iso


### Run your first tests

DVD installation

    # openqa-client isos post ISO=openSUSE-Leap-15.1-DVD-x86_64.iso DISTRI=opensuse VERSION=Leap FLAVOR=DVD ARCH=x86_64

### Start more workers

Depending on the number of cores **and available memory** (Recommended `4GB RAM` per worker!), you might want to start more workers

    ## Enable and start 4 workers (for 4 cores)
    
    # systemctl enable --now openqa-worker@1
    # systemctl enable --now openqa-worker@2
    # systemctl enable --now openqa-worker@3
    # systemctl enable --now openqa-worker@4

License
-------

MIT

Author Information
------------------

Felix Niederwanger, 2020