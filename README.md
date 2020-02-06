OpenQA
======

Role to install and bootstrap [open.qa](OpenQA) on a host

Requirements
------------

Basic `openSUSE` Linux installation with working network and `python-xml`

    zypper in python-xml

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.


Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: openqa }

Post-Install steps
------------------

The following steps need to be done manually after installing

### Download ISOs

ISOs to be tested should be stored in `/var/lib/openqa/share/factory/iso`

    # cd /var/lib/openqa/share/factory/iso
    # wget https://download.opensuse.org/distribution/leap/15.1/iso/openSUSE-Leap-15.1-NET-x86_64.iso

#### Run first test

# Run the first test

    # openqa-client isos post \
             ISO=openSUSE-Leap-15.1-NET-x86_64.iso \
             DISTRI=opensuse \
             VERSION=Leap \
             FLAVOR=NET \
             ARCH=x86_64

### Start more workers

Depending on the number of cores and available memory, you might want to start more workers

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