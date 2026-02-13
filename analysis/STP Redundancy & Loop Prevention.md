## What Was Happening

In this phase of the lab, I created a redundant Layer 2 path between two switches by connecting them with two trunk links.
While redundancy increases availability, it also introduces the risk of Layer 2 loops, which can lead to broadcast storms and complete network failure.
To manage this risk, Spanning Tree Protocol (STP) was enabled and manually tuned.
Switch0 was configured as the Root Bridge for VLAN 10 by lowering its bridge priority.

---

## What Stood Out in the Behavior

After configuring the root priority, the STP topology recalculated and a new logical tree was formed.
Switch0 successfully became the Root Bridge.
On Switch1, one of the trunk interfaces transitioned into the Root Port state (Forwarding), while the other redundant link moved into a Blocking (Alternate) state.
This clearly demonstrated that STP was actively preventing a Layer 2 loop.

One important observation was that before both trunk links were fully configured for VLAN 10, STP did not block any interface — because technically there was no loop detected. Once both links were active for the same VLAN, STP immediately recalculated and blocked the redundant path.

---

## Key Indicators

- Switch0 elected as Root Bridge  
- Bridge priority manually configured  
- One trunk link in Forwarding state  
- One redundant trunk link in Blocking state  
- No broadcast storm observed  

---

## Why This Matters

Layer 2 loops are extremely dangerous because Ethernet does not include a TTL mechanism like IP.
If STP is not functioning properly, a single misconfiguration can cause uncontrolled broadcast replication and bring down the entire network.
This lab clearly shows how STP dynamically selects the best path and disables redundant links while keeping them available as backup.

---

## Conclusion

The implementation confirms that STP is essential whenever redundant Layer 2 links exist.
By controlling root bridge election and verifying port states, I ensured the network remains both redundant and stable.
This phase demonstrates the importance of understanding not just how to configure redundancy, but how to control it safely.
