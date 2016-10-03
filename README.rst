simple isc-dhcp-server role
#############################

Just a simple ISC server DHCP role with failover option and without shared-network. (for now on.. coming soon)

Platforms
=========

Debian and Ubuntu

Requirements
==============

None

Playbook example
===================
::
    
   dhcp_interfaces: eth2
   dhcp_common_domain: evens.tld
   dhcp_common_nameservers: ns1.evens.tld, ns2.evens.tld
   dhcp_common_default_lease_time: 600
   dhcp_common_max_lease_time: 7200
   dhcp_log_facility: local7
   dhcp_authoritative: False
   dhcp_ddns_updates: on
   dhcp_ddns_updates_style: none
   
   dhcp_failover: epigateway-failover-dhcp
   dhcp_failover_primary: False
   ---
   dhcp_failover_secondary: True
   dhcp_failover_address: 192.168.23.1
   dhcp_failover_port: 520
   dhcp_failover_peer_address: 192.168.23.2
   dhcp_failover_peer_port: 520
   dhcp_failover_max_response_delay: 60
   dhcp_failover_max_unacked_updates: 10
   ---
   dhcp_failover_mclt: 3600
   dhcp_failover_split: 128
   
   dhcp_subnet_configuration:
   - subnet_base: 192.168.23.0
     subnet_netmask : 255.255.255.0
     
     subnet_pool: True
     subnet_pool_failover: epigateway-failover-dhcp
     subnet_pool_range_start: 192.168.23.50
     subnet_pool_range_end: 192.168.23.199
     subnet_pool_routers: 192.168.23.1
     subnet_pool_broadcast_address: 192.168.23.255
     subnet_pool_domain_name_servers: 192.168.23.2, 192.168.23.1, 8.8.8.8
     subnet_pool_domain_name: evens.tld
     subnet_pool_domain_search: evens.tld
     subnet_pool_ntp: 192.168.23.1
     subnet_pool_default_lease_time: 21600
     subnet_pool_max_lease_time: 36000
   
   dhcp_hosts_configuration:

   - name: vbox85
     mac_address: "08:00:ee:28:ge:33"
     fixed_address: debian85.evens.tld

   - name: vbox82c
     mac_address: "08:ee:27:3c:d5:bc"
     fixed_address: debian82c.evens.tld

    ...

License
=========

MIT_

.. _MIT: LICENSE

Author
=======

Evens SOLIGNAC - evenssolignac@live.fr
