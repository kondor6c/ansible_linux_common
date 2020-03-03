Role Name
=========

Very common across every system configurations. We set these kinds of parameters on almost every machine we manipulate. Some of these examples include:
- logging
- ssh config (banners ports)
- package repositories and updates
- core organization certificates
- NTP

While it could be argued that these could go into roles of their own, this is a jumping off point and if they are simple enough moving them to a different role just to insert an ntp configuration file seems like it might actually complicate things because you'd be looking at a separate role just to find that this role does one simple task. 

Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

BSD

Author Information
------------------
Kevin Faulkner
An optional section for the role authors to include contact information, or a website (HTML is not allowed).
cat vars/repos.yml  |yq '.yum_repos |.[] | select(.long_name | test(Centos* )  |not) | select(.gpg_key | test(EPEL* )  |not)' 
