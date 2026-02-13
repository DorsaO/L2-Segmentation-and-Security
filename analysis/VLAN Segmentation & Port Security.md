## What Was Happening

In this lab, I designed a small Layer 2 network using two switches and implemented VLAN segmentation to isolate different types of devices.
The goal was to separate users, servers, and administrative systems into different broadcast domains while also testing what would happen if a malicious device attempted to bypass Layer 2 restrictions.
The VLANs were configured as follows:

- VLAN 10 – Users  
- VLAN 20 – Servers  
- VLAN 30 – Admin  

After segmentation was complete, I introduced an attacker PC inside VLAN 10 to simulate suspicious Layer 2 behavior and observe how the switch responded when Port Security was enabled.

---

## What Stood Out in the Configuration

The first noticeable improvement after VLAN implementation was broadcast isolation. Devices in VLAN 10 could not directly communicate with devices in VLAN 20 or VLAN 30 without Layer 3 routing.

From a traffic perspective, this significantly reduces unnecessary broadcast propagation and improves both security and performance.
When Port Security was enabled on access ports, the switch began learning and locking MAC addresses per interface. I configured the maximum allowed MAC address to 1 with violation mode set to shutdown.

This meant that if another device attempted to use the same port (for example, by spoofing or physically replacing the machine), the switch would immediately disable the port.

---

## Attack Simulation

To simulate abnormal behavior, I used the attacker PC and attempted to trigger a security violation.

Once the switch detected a MAC address change beyond the allowed limit, the interface transitioned into an err-disabled state.
This behavior confirms that the port was successfully protected against unauthorized device changes.
In a real-world environment, this would prevent simple physical-layer attacks such as unplugging a legitimate user device and plugging in a rogue laptop.

---

## Key Indicators

- VLAN isolation between users, servers, and admin devices  
- Access ports configured with Port Security  
- Maximum MAC address limit enforced  
- Violation mode set to shutdown  
- Interface moved to err-disabled after violation  

---

## Conclusion

This lab demonstrates how basic Layer 2 segmentation combined with Port Security significantly strengthens internal network protection.
Even without advanced firewalls or IDS systems, properly configured VLANs and switch security features can prevent lateral movement and unauthorized physical access attempts.
The results confirm that segmentation is not just about organization — it is a foundational security control.
