# Kiss-Forward
> Premature abstraction is a result of procrastination and anxiety

While designing a new protocol, a significant amount of time is often wasted trying to choose the perfect encoding, compression, schema, cryptography, and so on. Chances are, you won't get it right the first time. Therefore, it is better to stick with something while maintaining a path for forward compatibility.

Many recent projects have chosen the Multiformats abstraction from Protocol Labs to address this issue. However, I argue that this approach is not ideal for several reasons:

1. It introduces more byte overhead than necessary.
2. It offers more abstraction than needed, which still requires attention.
3. As more formats are added, you will need to adopt even more bytes to support new formats.

As an alternative, this document describes how to stay forward-compatible while minimizing overhead. Are you ready for it?

## Spec

Add a prefix **Version byte**.

```md!
<version: 0-255> <...rest of your data>
```

That's it; that's the spec.

Still here? Alright, there are more examples, details, and ideas that might help.

#### Defaults for Known Lengths

When dealing with data of known length, such as public keys or signatures, it is helpful to omit the version byte and only add it if you ever require cryptographic agility. Chances are, your project will become obsolete much sooner.

In this scheme, if you are using ED25519 keys, any key encoded as 32 bytes in the future is assumed to be an ED25519 key. Newer versions are distinguished by the fact that they are not 32 bytes long.
