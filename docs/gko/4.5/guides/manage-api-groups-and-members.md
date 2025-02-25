---
description: Access control for APIs in APIM
---

# Manage API and Application Groups and Members

`ApiV4Definition`, `ApiDefinition`, and `Application` CRDs all support configuration of user permissions. This means that you can define the groups and members that can or cannot access a specific API or Application in APIM, and do this declaratively from a CRD.&#x20;

## Configuring Groups and Members

The syntax is the same for `ApiV4Definition`, `ApiDefinition`, and `Application` CRDs, with groups and members attributes at the root of the spec:

```yaml
 spec:
  groups:
    - developers
    - users
  members:
    - source: gravitee
      sourceId: my.name@bestproducts.com
      role: USER
    - source: gravitee
      sourceId: another.name@amce.com
      role: WRITER
  # [...]
```

Generally speaking, if a group or member referenced from an API or Application does not exist in APIM, that group or member is simply ignored and not added to the resource in APIM.&#x20;

{% hint style="info" %}
For APIs managed by GKO, you will not be able to add or modify groups or members manually from the API management console.
{% endhint %}

## Limitations

For APIs and Applications managed by GKO, the source of truth for groups and members should exclusively be what is defined in the CRD.&#x20;

However, in the Gravitee API Management Console, there are environment-level settings that can be used to automatically assign groups to every new API or application that gets created. These settings are shown in the screenshot below.

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

It is not recommend to use or to rely on these features for APIs or Applications managed by GKO. If used, these automatic groups will be added when an API is first created by the operator, but will be removed when changes are applied later on.
