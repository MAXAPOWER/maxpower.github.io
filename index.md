---
layout: default
---

[Thanks to Mad Hat for starting me up.](https://www.youtube.com/@madhatistaken)

# Preface

Why **Vulnerability Management**? Well, simply put, it coalesces three of the things I enjoy most about cybersecurity: **operating**, **analyzing**, and **engineering**. 

## Shell Begin[ning]s

> It's not who I am underneath; it's what I _do_ that defines me.

In my pwsh scripts, my first line of code always begins with my 'stylized' header comment: angled brackets and hashes, with the script title, my name (+ any collaborators), and the approximate date all piped together.

Following that, I'll comment in references to the source Nessus Plugin ID with the URL to the page in their Plugin DB. I might add any pertinent CVEs or CWEs (from NIST / MITRE) as appropriate.

```powershell
<# Title: Svc Path Quoter | Author: Max Soler | Date: December 2023 #>
### Nessus Plugin ID 63155| Reference: CVE-2014-0759 | https://nvd.nist.gov/vuln/detail/CVE-2014-0759 ###
```

Keeping it simple, right? If the sysads on the infra team take a cursory glance in the .ps1 file itself, they can immediately read in plain english what the script is for, which analyst they can contact if something is up, and the general dev date. Pragmatically, I would include versioning if it goes through CCB, but practically, the admins and analysts I've worked with just prefer to do a quick check to see if date is more recent than another.

### Tenable Nessus Report

Tenable Nessus's Plugin ID 63155, titled [Microsoft Windows Unquoted Service Path Enumeration](https://www.tenable.com/plugins/nessus/63155), neatly gives the 'tl;dr' upfront:

![Synopsis](https://github.com/MAXAPOWER/maxpower.github.io/blob/main/nessus%20synopsis.png)
> **Synopsis** | The remote Windows host has at least one service installed that uses an unquoted service path.

So I'm going to leverage PowerShell's native _#requires_ feature to require pwsh v5.1 as the minimum required WMF version. I'm also going to add a second _#requires_ statement with the arg _-runasadministrator_, as another failsafe.

```powershell
#requires -version 5.1
#requires -runasadministrator
```

Now with that, there's maybe a not-so-necessary preference I like to sort out. Since I'm often moving pwsh code/cmdlets from local guest VM to instance, or local ISE to VS Code, or Code to pipeline

#### The Prereqs

*   Windows security policies
*   Local computer policies (for example, Deny access to this computer from the network, Access this computer from the network)
*   Antivirus or endpoint security rules
*   IPS/IDS

To avoid too many complications, I'm going to break the rest of the script block into a function that will be driven by an if condition. This pretty much follows what was SOP for my last gig:

1.  The sysads run the org's .wim.
2.  The vuln analyists scan and stig.
3.  Then, the req floodgates open.
