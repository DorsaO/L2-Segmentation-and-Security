## What Was Happening

In this lab, I designed a small Layer 2 network using two switches and implemented VLAN segmentation to isolate different types of devices.

The goal was to separate users, servers, and administrative systems into different broadcast domains while also testing what would happen if a malicious device attempted to bypass Layer 2 restrictions.

The VLANs were configured as follows:

- VLAN 10 – Users  
- VLAN 20 – Servers  
- VLAN 30 – Admin  

📷 See topology diagram:  
`screenshots/topology.png`


## VLAN Configuration Verification

After creating the VLANs and assigning access ports, I verified the configuration on both switches.

📷 Switch0 VLAN table:  
`screenshots/SW0-VLAN-Table.png`

📷 Switch1 VLAN table:  
`screenshots/SW1-VLAN-Table.png`

The VLAN tables confirm that devices are correctly assigned to their respective broadcast domains.


## Port Security Implementation

Port Security was enabled on access ports with the following configuration:

- Maximum MAC address set to 1  
- Violation mode set to shutdown  

📷 Port Security configuration:  
`screenshots/port-security-config.png`

📷 Port Security status verification:  
`screenshots/port-security-status.png`

When enabled, the switch dynamically learned the MAC address of the connected device and restricted additional MAC addresses on the same port.


## Attack Simulation

To simulate abnormal behavior, I introduced an attacker device and triggered a security violation.

Once the switch detected a MAC address change beyond the allowed limit, the interface transitioned into an err-disabled state.

📷 Violation test result:  
`screenshots/violation-test.png`

This confirms that unauthorized device replacement or MAC spoofing attempts are effectively blocked.


## Key Indicators

- VLAN isolation between users, servers, and admin devices  
- Access ports protected with Port Security  
- MAC address limit enforced  
- Interface automatically disabled after violation  


## Conclusion

This phase demonstrates how proper Layer 2 segmentation combined with Port Security significantly strengthens internal network protection.
Even without advanced security appliances, correctly configured switches can prevent lateral movement and unauthorized physical access attempts.
Segmentation is not just organizational — it is a core security control.
