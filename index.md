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

#### Header 4

*   This is an unordered list following a header.
*   This is an unordered list following a header.
*   This is an unordered list following a header.

##### Header 5

1.  This is an ordered list following a header.
2.  This is an ordered list following a header.
3.  This is an ordered list following a header.

###### Header 6

| head1        | head two          | three |
|:-------------|:------------------|:------|
| ok           | good swedish fish | nice  |
| out of stock | good and plenty   | nice  |
| ok           | good `oreos`      | hmm   |
| ok           | good `zoute` drop | yumm  |

### There's a horizontal rule below this.

* * *

### Here is an unordered list:

*   Item foo
*   Item bar
*   Item baz
*   Item zip

### And an ordered list:

1.  Item one
1.  Item two
1.  Item three
1.  Item four

### And a nested list:

- level 1 item
  - level 2 item
  - level 2 item
    - level 3 item
    - level 3 item
- level 1 item
  - level 2 item
  - level 2 item
  - level 2 item
- level 1 item
  - level 2 item
  - level 2 item
- level 1 item

### Small image

![Octocat](https://github.githubassets.com/images/icons/emoji/octocat.png)

### Large image

![Branching](https://guides.github.com/activities/hello-world/branching.png)


### Definition lists can be used with HTML syntax.

<dl>
<dt>Name</dt>
<dd>Godzilla</dd>
<dt>Born</dt>
<dd>1952</dd>
<dt>Birthplace</dt>
<dd>Japan</dd>
<dt>Color</dt>
<dd>Green</dd>
</dl>

```
Long, single-line code blocks should not wrap. They should horizontally scroll if they are too long. This line should be long enough to demonstrate this.
```

```
The final element.
```
