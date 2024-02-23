---
Title: Embedded VRKai Webpage Metadata Standard
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

Inside of any html webpage, one must include a single meta tag with the name `shinkai-embedding-vrkai` in the `head`. Inside of the `content` of this meta tag, we include a JSON list (as a string) which holds one or more elements that point to a VRKai file.

Thus this is a pseudo-code example of the head to use this standard:

```
<head>
    <meta name="shinkai-embedding-vrkai" content="[JSON List]">
</head>

```

### Types Of VRKai Elements

As mentioned the json object within the meta tag content must be a JSON list at the top level. Inside the list it can hold one of three types of elements:

#### Direct

A direct element holds a base64-encoded VRKai file inside of it directly (in the `vrkai-content` field). It generally isn't recommended to put this much data into the head, however support is provided for use cases where this is needed (ex. unique packaging setups that need more portability).

Example JSON:
```json
<
    "vrkai-type": "direct",
    "vrkai-content": "..."
    "metadata": null
>
```

#### HTTP Reference

A HTTP reference element points to an external URL where a `.vrkai` file is hosted on the internet.

```json
<
    "vrkai-type": "http",
    "url": "http://my-website.com/link/to/VR.vrkai"
    "metadata": null
>
```

#### Network Reference

Network references allow specifying a path into the Vector File System of a Shinkai Node on the Shinkai Network. It supports both pathing to a specific item (which holds equivalent data as a single VRKai file) or even a folder with many.

Of note, just because a path onto the network is provided, does not per-say mean that said path has public permissions set for it which allows anyone to read. The provided path may alternatively have "Whitelist" permission set, and require Kai delegation in order to gain access.

```json
<
    "vrkai-type": "network",
    "network-path": "@@rob.shinkai/profileName/vectorFS/path/to/folder/or/item"
    "metadata": null
>
```

##### Metadata Field

All elements above include a `metadata` field. This field is set to `null` by default, or holds an arbitrary string with data. It is included as preparation for the future/allowing advanced use cases such as allowing a single webpage to mark each vrkai with extra information such as denoting hierarchy, which VRs should be put in separate folders together, or anything else that helps in processing/saving these into a Shinkai Node's VectorFS.

### HTML Example

Here is a compiled example of a filled out meta tag using all three types of elements:

```html
<head>
    <meta name="shinkai-embedding-vrkai" content='[{"vrkai-type": "direct", "content": "...", "metadata": null}, {"vrkai-type": "http", "url": "http://my-website.com/link/to/VR.vrkai", "metadata": null}, {"vrkai-type": "network", "network-path": "@@rob.shinkai/profileName/vectorFS/path/to/folder/or/item", "metadata": null}]'>
</head>
```

## Rationale

<!-- Further explanation about choices made in the specification, links to external relevant content/work, and anything else to wrap up the SHIP. -->

## Copyright

Copyright and related rights waived via [CC0](../LICENSE.md).
