############
Linux Common
############

Very common automation actions across every system configurations. 
We set these kinds of parameters on almost every machine we manipulate. Some of these examples include:
  * logging
  * ssh config (banners ports)
  * package repositories and updates
  * organization certificates
  * NTP
  * users, groups and sudo 

While it could be argued that these could go into roles of their own, this is a jumping off point and if they are simple enough moving them to a different role just to insert an NTP configuration file seems like it might actually complicate things because you'd be looking at a separate role just to find that this role does one simple task.
I try to consider this an "incubating" role. Where you can add content, and move it out when you deem neccessary.

Trends and patterns
-------------------
setype is generally considered and tried to be used when possible


Motives
-------
I wanted to define configuration as variables. Which often meant that complex dictionaries were used and handling them. A missing attribute or modifying a nested value is not easily done in Ansible.
With that in mind I hesitated greatly on the complexity/difficulty that it brings. I tried very hard to create good safe defaults. For more information on these look at Data Structures 

************
Requirements
************
Ansible >= 2.8
Fedora or CentOS or RHEL
Ubuntu


**************
Role Variables
**************
Sensible defaults are defined and prevent this role from failing. Even if you run this role on an internal company's systems. This role will work on a standard Linux install, perhaps at your home.
This is a critical design step, the reasoning was that if this role could setup a system that isn't tied to many dependencies of an enterprise company a new sysadmin/operator might feel more comfortable to
experiment and maintain/extend the automation instead of fearing breaking something that can only be ran on a corporate system.

The disadvantage of this is that the variables tend to be complex. Where I tried to handle both use cases of a corporate Centos 7 machine and a home Fedora machine simultaneously 
a personal private cloud mail server running Ubuntu (and maybe sometime soon, a home arm64 machine running gentoo or arch).
Some of the variables are using lists of dicts, this is mostly to help with organization. For example the repositories:
``cat defaults/main.yml  |yq '.yum_repos[] | select(.long_name | test(Centos* )  |not) | select(.gpg_key | test(EPEL* )  |not)' ``

Data Structures
---------------

.. code-block: yaml
   net_hosts:
     - interfaces:
         - hwaddr: 10:1f:74:3d:12:ef
           address: 10.1.1.69
           name: foo
         - hwaddr: aa:bb:cc:dd:ee:ff
           address: 10.1.1.69
           name: foo
       domain: localnet
       group: example_host
       services:
         - ssh
       tags:
         - multi_interface_bond_br
     - interfaces:
         - address: 10.1.2.1
           hwaddr: 11:22:33:44:55:66
           name: server
       domain: localnet
       tags:
         - regular_machine
     - interfaces:
         - address: 127.0.0.1
           name: pixel
       domain: rubiconproject.com
       tags:
         - example_of_etc_hosts_workaround

Dependencies
------------
none

Example Playbook
----------------
.. code-block: yaml
   


License
-------
BSD

Author Information
------------------
Kevin Faulkner

TODO
----
- generic systemd service unit, and dict that exposes: /path/exec options ...  (one shot kind of thing)
- systemd generator for cron's
- basic cloudinit
- chroot 'connection' compatability 
- write out kickstart script with repos, write out bash heredoc or again utilize cloudinit
- maintenance: upgrade all packages that will not require reboot. This will go hand in hand with the other service that allows notifying/restarting services that have been upgraded

new features
############
- deb based distributions, split common linux and rpm out
- user files
- systemd networkd
- etc/hosts hacks

