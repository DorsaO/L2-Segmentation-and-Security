# L2-Segmentation-and-Security
Layer 2 network segmentation and security implementation using VLAN, STP, and Port Security.

This is a project I worked on to get some hands-on experience with Layer 2 networking and security. My goal was to build a small, realistic switched network and see how things like VLANs, Spanning Tree Protocol (STP), and Port Security actually work when you're trying to protect an internal network.

## Project Objectives
I set out to accomplish a few specific things in this lab:

 * Set up network segmentation using VLANs.

 * Configure trunk links to connect my switches.

 * Take control of the STP root bridge election.

 * Make sure redundant links didn't cause network loops.

 * Lock down access ports using Port Security.

 * Simulate a security violation to see the defense mechanisms in action.

## My Network Design
<img width="794" height="534" alt="topology" src="https://github.com/user-attachments/assets/9ce596dc-d132-4a77-b00a-e8115118b773" />

For this lab, I connected two switches using redundant trunk links. I decided to split the network into three different broadcast domains to keep things organized and secure:



VLAN 10 – Users 


VLAN 20 – Servers 


VLAN 30 – Admin 

I intentionally added extra links between the switches so I could test how the network handles redundancy without crashing.

## VLANs & Port Security
I separated the users, servers, and admins into their own VLANs so they couldn't just see each other's traffic by default. To make the access ports more secure, I configured Port Security with these rules:


Max MAC addresses: Limited to 1.


Violation Mode: Set to "shutdown".

I even simulated an attack where an unauthorized device tried to connect. It was cool to see the interface immediately go into an "err-disabled" state, effectively blocking the threat. You can find my full notes on this in analysis/VLAN-Segmentation-Port-Security.md.


## STP & Loop Prevention
Redundancy is great for uptime, but it can cause loops if you aren't careful. I manually configured Switch0 as the Root Bridge by changing its priority. After that, I watched STP do its job:


It picked the best path for traffic.

It automatically blocked the redundant link to stop loops.

It kept the network stable even with multiple physical paths.

My detailed analysis of this is in analysis/STP-Redundancy-Loop-Prevention.md.

## Project Structure

 * analysis/ – My technical observations and what I learned.


 * configs/ – The full configuration files for the switches.


 * screenshots/ – Proof of the commands and verification outputs.


 * diagrams/ – The topology files showing how everything is connected.


## What I Learned
Doing this lab helped me practice some essential networking skills:

Designing and implementing VLANs.

Controlling STP behavior instead of just leaving it to chance.

Hardening switches against basic Layer 2 attacks.

Troubleshooting when things didn't work as expected.


### Key Takeaway: Layer 2 security isn't just an "extra" feature—it's the foundation. Even a small mistake in a switch configuration can lead to a total network outage or a security hole. This project really showed me why understanding these fundamentals is so important for real-world networking.
