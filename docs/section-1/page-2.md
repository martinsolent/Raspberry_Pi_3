---
title: Stuff 1
parent: Section 1
layout: default
nav_order: 2
---

# Section 1 - Stuff 1

Default label
{: .label }

Blue label
{: .label .label-blue }

Stable
{: .label .label-green }

New release
{: .label .label-purple }

Coming soon
{: .label .label-yellow }

Deprecated
{: .label .label-red }


- [ ] hello, this is a todo item
- [ ] hello, this is another todo item
- [ ] goodbye, this item is done


```mermaid
graph TD;
    accTitle: the diamond pattern
    accDescr: a graph with four nodes: A points to B and C, while B and C both point to D
    A-->B;
    A-->C;
    B-->D;
    C-->D;
```