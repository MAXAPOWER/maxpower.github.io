---
layout: default
---

[Thanks to BAE for giving me a chance.](https://www.baesystems.com/en/home)

# Preface

Why **Vulnerability Management**? Well, simply put, it coalesces three of the things I enjoy most about cybersecurity: **operating**, **analyzing**, and **engineering**. 

## Shell Begin[ning]s

> It's not who I am underneath; it's what I _do_ that defines me.

### Tenable Nessus Guidance

Following along Tenable Nessus's guide to [Credentialed Checks on Windows](https://docs.tenable.com/nessus/Content/CredentialedChecksOnWindows.htm), the first note reads:

![Note](https://github.com/MAXAPOWER/maxpower.github.io/blob/e871f81e671794ef5c6e5bb6ed358d2165694781/tenable%20note.png)

So I'm going to leverage PowerShell's native _#requires_ feature to require pwsh v5.1 (I know Tenable says 5.0, but I'm stipulating 5.1 since Win10 ships with it by default) as the minimum required WMF version. I'm also going to add a second _#requires_ statement with the arg _-runasadministrator_, to follow the advice of a few good sysads (namely to prevent accidental execution by a user, if the scope of the execpol is messed around with). 

```powershell
#requires -version 5.1
#requires -runasadministrator
```
TODO: Maybe come back and revisit a simple CIM obj / WMI query for Windows numeric release version, since Tenable Nessus only officially supports Windows 10 and greater.

Now with that, there are some more necessary bits we have to sort out. And this is where the fork in the road comes in...

#### The Prereqs

*   Windows security policies
*   Local computer policies (for example, Deny access to this computer from the network, Access this computer from the network)
*   Antivirus or endpoint security rules
*   IPS/IDS

To avoid too many complications, I'm going to break the rest of the script block into a function that will be driven by an if condition. This pretty much follows what was SOP for my last gig:

1.  The sysads run the org's .wim.
2.  The vuln analyists scan and stig.
3.  Then, the req floodgates open.
