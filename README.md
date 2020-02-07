# OpenQA

Role to install and bootstrap [open.qa](OpenQA) for [openSUSE Linux](https://opensuse.org/)

## Requirements

A basic openSUSE Linux installation with internet connectivity and installed `python-xml` (Required for the ansible [zypper module](https://docs.ansible.com/ansible/latest/modules/zypper_module.html))

    zypper in python-xml

## Role Variables

The following variables are set

    firewall_configure: true           # Enable firewall configuration
    firewall_interface: "public"       # Firewall interface to configure


## Example Playbook

    - hosts: servers
      roles:
         - { role: openqa, firewall_configure: true }

## Post-Install steps

Checkout the [OpenQA Documentation](http://open.qa/docs/#_adding_a_new_iso_to_test) for the first steps after installing. The following is just a jump-start guide.

### Configure API keys

You find the API keys in your web frontend. Configure your client by editing either `/etc/openqa/client.conf` (global config) or `~/.config/openqa/client.conf` (user config).
Set the API key and API secret accordingly.

    $ mkdir -p ~/.config/openqa/
    $ vim ~/.config/openqa/client.conf
    
    [localhost]
    key = 1234567890ABCDEF
    secret = 1234567890ABCDEF


### Download ISOs

ISOs to be tested should be stored in `/var/lib/openqa/share/factory/iso`. Download your first iso 

    # wget -P /var/lib/openqa/share/factory/iso/ https://download.opensuse.org/distribution/leap/15.1/iso/openSUSE-Leap-15.1-DVD-x86_64.iso


### Run your first tests

Run a **full product test** for a DVD

      $ openqa-client isos post ISO=openSUSE-Leap-15.1-DVD-x86_64.iso DISTRI=opensuse VERSION=Leap FLAVOR=DVD ARCH=x86_64

Run a **single test**

      $ openqa-client jobs post ISO=openSUSE-Leap-15.1-DVD-x86_64.iso DISTRI=opensuse VERSION=Leap FLAVOR=DVD ARCH=x86_64 TEST=lvm MACHINE=64bit

### Start more workers

Depending on the number of cores **and available memory** (Up to `4GB RAM` per worker!), you might want to enable more workers

      ## Enable and start 4 workers (4 cores)
      # systemctl enable --now openqa-worker@1
      # systemctl enable --now openqa-worker@2
      # systemctl enable --now openqa-worker@3
      # systemctl enable --now openqa-worker@4

## License


[GPLv2](https://opensource.org/licenses/gpl-2.0.php)