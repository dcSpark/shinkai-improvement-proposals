---
Title: VRKai Web Head Standard
Status: Draft
Authors:
  - Robert Kornacki <rob@shinkai.com>
Created: 2024-02-13
---

## Abstract

<!-- A short  description of the target goals and technical obstacles. -->

## Motivation

<!-- A more detailed description of the problem and its context with sufficient background to explain why this needs to be solved. -->

## Specification

```
<vrkai> [json] </vrkai>
```

The json object within the vrkai tags must be a JSON list at the top level. Inside the list it can hold one of three types of elements:

#### Direct

```json
<
    "vrkai-type": "direct",
    "content": "[Vector Resource JSON]"
>
```

#### HTTP Reference

```json
<
    "vrkai-type": "http-ref",
    "url": "http://my-website.com/link/to/VR.vrkai"
>
```

#### Network Reference

Network references allow specifying a path to a node on the Shinkai Network, directly to specific item (which holds a single Vector Resource) or even a folder with many.

Of note, just because a path onto the network is provided, does not per-say mean that said path has public permissions set for it. The provided path may have "Whitelist" permissions, and require delegation in order to gain access.

```json
<
    "vrkai-type": "network-ref",
    "network-path": "@@rob.shinkai/path/to/folder/or/item"
>
```

## Rationale

<!-- Further explanation about choices made in the specification, links to external relevant content/work, and anything else to wrap up the SHIP. -->

## Copyright

Copyright and related rights waived via [CC0](../LICENSE.md).
