CCNA Lab | Spanning Tree Protocol (STP) Convergence & Link Failure Recovery

Today I completed a hands-on lab to understand how Spanning Tree Protocol (STP) maintains a loop-free Layer 2 network while ensuring redundancy.

In this lab, I first created a network with three interconnected switches and verified the Root Bridge election using the show spanning-tree command. STP automatically blocked one redundant link to prevent switching loops.

To test STP's fault tolerance, I intentionally disconnected an active link between the switches. Within seconds, STP recalculated the topology and activated the previously blocked backup link, restoring network connectivity without creating a loop. After reconnecting the original link, STP converged again and returned the redundant path to the Blocking state.

Key concepts practiced:

✅ Root Bridge Election
✅ Root Port & Designated Port Selection
✅ Blocking Redundant Links
✅ STP Convergence After Link Failure
✅ Automatic Failover to Backup Path
✅ Loop Prevention & Network Redundancy
✅ Verification Using Cisco IOS Commands

This lab demonstrated why STP is essential in enterprise networks—it provides high availability through redundant links while preventing broadcast storms, MAC address table instability, and Layer 2 loops.
