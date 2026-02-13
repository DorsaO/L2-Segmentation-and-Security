## What Was Happening

In this phase of the lab, I introduced redundancy by connecting two switches with two trunk links.

While redundancy improves availability, it also creates the risk of Layer 2 loops, which can lead to broadcast storms and complete network instability.

Spanning Tree Protocol (STP) was enabled and manually tuned to control the topology.


## Trunk Configuration Verification

Both inter-switch links were configured as trunk ports to carry multiple VLANs.

📷 Switch0 trunk status:  
`screenshots/SW0-Trunk-Status.png`

📷 Switch1 trunk status:  
`screenshots/SW1-Trunk-Status.png`

The trunk outputs confirm that VLAN 10 is allowed and active across both links.


## Root Bridge Election

Switch0 was manually configured as the Root Bridge by lowering its bridge priority.

After STP recalculation:

📷 Root verification on Switch0:  
`screenshots/SW0-STP-VLAN10-Root.png`

The output confirms that Switch0 is acting as the Root Bridge for VLAN 10.


## Loop Prevention in Action

Since two trunk links exist between the switches, STP must block one of them to prevent a Layer 2 loop.

On Switch1:

📷 Blocking port verification:  
`screenshots/SW1-STP-VLAN10-Blocking.png`

One interface remains in Forwarding state (Root Port), while the redundant link transitions to Blocking (Alternate) state.

This confirms that STP is actively preventing broadcast loops.


## Why This Matters

Layer 2 loops are especially dangerous because Ethernet does not include a TTL mechanism like IP.

Without STP, frames could circulate indefinitely, causing network congestion and outages.

This lab clearly demonstrates how STP dynamically builds a loop-free topology while maintaining redundancy.


## Key Indicators

- Switch0 elected as Root Bridge  
- Manual bridge priority configuration  
- One trunk link forwarding  
- One trunk link blocked  
- No broadcast storm observed  


## Conclusion

This phase confirms that STP is essential whenever redundant Layer 2 links exist.

By controlling root bridge election and verifying port states, the network remains both redundant and stable.

Redundancy without control is dangerous — STP ensures redundancy remains safe.
