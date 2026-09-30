# Port-Security-Lab


A Layer 2 security lab that uses Port Security on a Cisco switch to limit which devices can connect to each access port. If an unauthorized device connects, the port reacts based on the configured violation mode (shutdown, restrict, or protect).

Topology
Device	   Switch Port	         Notes
PC0      	 Fa0/1	Port security enabled
PC1        Fa0/2	Port security enabled

Place both PCs in the same subnet (for example 192.168.1.10/24 and 192.168.1.20/24).

Configuration
enable
configure terminal
hostname Switch1

interface range FastEthernet0/1 - 2
 switchport mode access
 switchport port-security
 switchport port-security maximum 1  ( accept only 1 mac address )
 switchport port-security mac-address sticky   ( memorizing mac address )
 switchport port-security violation shutdown ( Puts the port in err-disabled state on a violation )
 no shutdown
end
write memory

Verification
show port-security
show port-security interface fastEthernet 0/1
show port-security address
show interfaces status
