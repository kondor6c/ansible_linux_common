Linux Common
============

Very common across every system configurations. We set these kinds of parameters on almost every machine we manipulate. Some of these examples include:
- logging
- ssh config (banners ports)
- package repositories and updates
- organization certificates
- NTP
- users, groups and sudo 

While it could be argued that these could go into roles of their own, this is a jumping off point and if they are simple enough moving them to a different role just to insert an ntp configuration file seems like it might actually complicate things because you'd be looking at a separate role just to find that this role does one simple task. 

Requirements
------------
RPM based distrubution

Role Variables
--------------
cat vars/repos.yml  |yq '.yum_repos |.[] | select(.long_name | test(Centos* )  |not) | select(.gpg_key | test(EPEL* )  |not)' 


Dependencies
------------
none

Example Playbook
----------------


License
-------

BSD

Author Information
------------------
Kevin Faulkner

TODO
----

new features
############
- deb based distributions, split common linux and rpm out
- user files
- systemd networkd
