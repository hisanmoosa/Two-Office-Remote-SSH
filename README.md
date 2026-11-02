# Two-office remote SSH | Project 10
Manage the Cork router from Dublin-PC using SSH version 2. This Cisco Packet Tracer lab builds on the two-office OSPF network and retains the extended ACL from Project 9.

![Two-office topology](images/topology.png)

## Demonstrated
- Reachability from Dublin-PC to Cork router address 10.0.0.2 (0% loss reported).
- Local username authentication and SSH v2 configuration on R2-CORK.
- Remote interface checks after SSH login.
- Privileged EXEC access using a separate enable secret.
- Telnet connection closed without a login; VTY lines allow SSH only.

## How it works
The local account netadmin logs into user EXEC mode (>). The enable secret allows entry into privileged EXEC mode (#), from which configuration mode can be entered. Both passwords belong to the same SSH session; this is not multifactor authentication. SSH encrypts the management connection. It does not encrypt all traffic between the offices.

## Network
| Device/interface | IP address |
|---|---|
| Dublin-PC | 192.168.10.11/24; gateway 192.168.10.1 |
| R1-dublin G0/0 | 192.168.10.1/24 |
| R1-dublin G0/1 | 10.0.0.1/30 |
| R2-CORK G0/1 | 10.0.0.2/30 — SSH target |
| R2-CORK G0/0 | 192.168.20.1/24 |
| Cork-PC | 192.168.20.11/24; gateway 192.168.20.1 |
| Dublin-Web | 192.168.10.20/24; gateway 192.168.10.1 |

OSPF area 0 provides routing. ACL 100 remains inbound on Cork G0/0, denying Cork-PC ping requests to Dublin-Web and permitting other IP traffic. It does not restrict SSH to a particular management source.

## Open and reproduce
Open [Project-10-Remote-SSH.pkt](lab/Project-10-Remote-SSH.pkt) in Packet Tracer. Follow [SSH setup instructions](configs/SSH-Setup-Reference.txt). From Dublin-PC, enter `ssh -l netadmin 10.0.0.2` (lowercase L). Use the public lab examples CorkLab10 for login and AdminLab10 after enable. Do not reuse these credentials outside this isolated lab.

[Router configurations](configs/) · [Test evidence](tests/Verification.txt) · [Combined evidence JPG](images/Project-10-Network-Evidence.jpg)

## Evidence scope
The .pkt and topology screenshot are preserved unchanged. The .pkt was not independently executed or inspected internally during packaging. Router configuration transcriptions preserve supplied statements and omit repeated blank separators. Test panels are recreated from learner-supplied text, not CLI screenshots. A 2048-bit RSA modulus was instructed, but key-size output was not supplied; RSA private keys are not part of the text configuration exports. Reproducing from text requires generating a new key pair.
