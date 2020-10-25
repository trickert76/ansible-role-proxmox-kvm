# ansible-role-proxmox-kvm

This role can be used to assign to all KVMs in an inventory. If the KVM is not yet present, it will be bootstraped via Debian preseed. Otherwise (the KVM exists) nothing happens.

So this role ensures, the KVM really exists.

So, this is an example playbook

    - name: "Check VMs on Proxmox"
      hosts: vms
      gather_facts: no
      roles:
        - trw.proxmox-kvm

Because the role needs to know a lot about the KVM here is a list of necessary facts per KVM.

This role only supports Debian (for now).

## Role variables:

`pve_api_username` user to access the Proxmox API

`pve_api_password` password for the user to access the Proxmox API

`pve_guest_hostgroup` name of the group where all Proxmox hosts are defined

`pve_guest_host` is the name of the host, where the KVM should be created on, otherwise the role uses the first host in the proxmox group

`domain` is the domain, where the VM is in. This is used for dns resolver as the default domain

`ntp_area` is the zone, where the KVM is located

`ntp_timezone` the timezone of the KVM

`pve_guest_locale` the default locale of the KVM

`pve_guest_keymap` the default keymap of the KVM

`users` is a dictonary containing at least one sub element `users.root.password` which is the default root password. Also you can define `users.root.allowed_keys` which is a list of SSH Pubkeys for the root user. The password and the pubkeys will be set during KVM creation.

If `net_ipv4` is defined with `dhcp` then the network is configured with router settings. Otherwise if is set to `static` then you need to define `net_ipv4_address`, `net_ipv4_netmask`, `net_ipv4_gateway` and `net_ipv4_dns`. The last one is a comma separeted list as string.

If `net_ipv6` is defined with `auto` then the network is configured with router settings. Otherwise if is set to `static` then you need to define `net_ipv6_address`, `net_ipv6_prefix`, `net_ipv6_gateway` and `net_ipv6_dns`. The last one is a comma separeted list as string.
 
