Ansible roles for running IPv6-mostly and IPv6-only on OpenWRT
==============================================================

This repository holds a collection of roles used to provision a OpenWRT device
with NAT64, PREF64 and DNS64 in order to run IPv6-mostly or IPv6-only network
behind such router.

It has been developed using [GL.iNet
AC1300](https://openwrt.org/toh/gl.inet/gl-a1300) running [OpenWRT
23.05.2](https://openwrt.org/releases/23.05/notes-23.05.2). Some adjustments
might be necessary for other devices and/or OpenWRT versions.

Please note that the roles are only adjusting the configuration. Services are
not restarted services in order to avoid unexpected disruptions. A complete
reboot is recommended after provisioning in order to make sure everything
starts properly.

Available roles
---------------

 - `openwrt-lan6`: sets up a second IPv6-only LAN interface
 - `openwrt-jool`: sets up Jool as a NAT64 in it's own network namespace
 - `openwrt-pref64`: sets up pref64 flag in router advertisements
 - `openwrt-dhcp108`: sets up DHCP option 108 (IPv6-only-preferred)
 - `openwrt-unbound`: sets up Unbound as a recursive resolver (to provide DNS64)


There are example playbooks showing how to invoke such a role.

Bootstrapping the router
------------------------

Run a clean installation of OpenWRT. Setup upstream connectivity if necessary.
Install `openssh-sftp-server` package. This can be also done with
`bootstrap.yml` playbook (see below). Don't forget to set `root` password before exposing the router.

How to run the playbooks
------------------------

Adjust inventory file. Make sure to put your router(s) into `openwrt` group.

Install the pre-requisites:

```
ansible-galaxy install -r requirements.yml -f
```

Now run the applicable playbooks for your router, for example:

```
ansible-playbook -i inventory.ini --limit openwrt bootstrap.yml lan6.yml wifi.yml jool.yml pref64.yml dhcp108.yml unbound.yml
```

Reboot the router. If everything went well it should start with all services
properly running.
