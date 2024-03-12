---
Title: Embedded VR Webpage Standard
Status: Draft
Authors:
  - Robert Kornacki <rob@shinkai.com>
Created: 2024-03-12
---

## Abstract

<!-- A short  description of the target goals and technical obstacles. -->

## Motivation

With this standard applications, crawlers, or extensions like Shinkai Visor will be able to auto-detect if the current webpage has pre-generated Vector Resources available for users to start using immediately. This allows for entirely new UX flows, where even a large group of 10+ documents can be loaded in mere seconds as pre-generated VRKai files, rather than the 5+ minutes it would take to generate them from scratch normally.

In Shinkai Visor specifically, this enables new opportunities such as providing VRKai files for the wiki/faq of an online browser-based game, and allow players to instantly ask questions they run into without having to even switch the tab.

## Specification

Inside of the `head` of any html webpage, one must include a single meta tag with the name `shinkai-vector-resources`. Inside of the `content` of this meta tag, we include a JSON list (as a string) which holds one or more elements which point to Vector Resources.

Thus this is a pseudo-code example of the standard:

```
<head>
    <meta name="shinkai-vector-resources" content="[JSON List Of Elements]">
    ...
</head>

```

### Types Of Elements

As mentioned the json object within the meta tag content must be a JSON list at the top level. Inside the list it can hold one of the following types of elements:

#### HTTP Reference

A HTTP reference element points to an external URL where a `.vrkai` or `.vrpack` file is hosted on the internet. Unlike direct elements, the url itself contains the file extension, which allows for differentiating between the two automatically.

Example JSON:

```json
{
  "element-type": "http",
  "url": "http://my-website.com/link/to/VR.vrkai",
  "metadata": null
}
```

#### Direct VRKai

A direct element which holds a base64-encoded VRKai file inside of it directly (in the `content` field). It generally isn't recommended to put this much data into the head, however support is provided for use cases where this is needed (ex. unique packaging setups that need more portability).

Example JSON:

```json
{
  "element-type": "direct-vrkai",
  "content": "...",
  "metadata": null
}
```

#### Direct VRPack

A direct element which holds a base64-encoded VRPack file inside of it directly (in the `content` field).

Example JSON:

```json
{
  "element-type": "direct-vrpack",
  "content": "...",
  "metadata": null
}
```

#### Network Reference

Network references allow specifying a path into the Vector File System of a Shinkai Node on the Shinkai Network. It supports both pathing to a specific item (which holds equivalent data as a single VRKai file) or even to a folder with many (which holds equivalent data as a VRPack file).

JSON Example:

```json
{
  "element-type": "network",
  "network-path": "@@rob.shinkai/profileName/vectorFS/path/to/folder/or/item",
  "metadata": null
}
```

Of note, just because a path onto the network is provided, does not per-say mean that said path has public permissions set for it (which allows anyone to have read access). For example, the provided path may have "Whitelist" permission set, and require Kai delegation in order to gain access.

##### Metadata Field

All elements above include a `metadata` field. This field is set to `null` by default, or can hold an arbitrary string with data. It is included for future-preparedness sake, allowing advanced use cases where further details are required to be taken into account while processing/saving the Vector Resources.

### HTML Example

Here is a compiled example of a meta tag using the various types of elements:

```html
<head>
  <meta
    name="shinkai-vector-resources"
    content='[{"element-type": "direct-vrkai", "content": "...", "metadata": null}, {"element-type": "http", "url": "http://my-website.com/link/to/VR.vrkai", "metadata": null}, {"element-type": "network", "network-path": "@@rob.shinkai/profileName/vectorFS/path/to/folder/or/item", "metadata": null}]'
  />
</head>
```

## Rationale

<!-- Further explanation about choices made in the specification, links to external relevant content/work, and anything else to wrap up the SHIP. -->

## Copyright

Copyright and related rights waived via [CC0](../LICENSE.md).
