Ansible roles for running IPv6-mostly and IPv6-only on OpenWRT
==============================================================

This repository holds a collection of roles used to provision a OpenWRT device
with NAT64, PREF64 and DNS64 in order to run IPv6-mostly or IPv6-only network
behind such router.

More documentation to come later.


### Running the role

Assuming that you have a router with working IPv:w

```
ansible-galaxy install -r requirements.yml -f
# Now run the applicable playbooks for your router, for example
ansible-playbook -i inventory.ini --limit openwrt lan6.yml jool.yml
```
