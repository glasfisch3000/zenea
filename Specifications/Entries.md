# Entry Storage
An entry's header information is stored in a single Data Layer block.
The hash of that block is used as the entry's ID which is not included in the block.
The entry's payload, if it exists, is stored in one or more blocks whose hashes are included in the entry header. In this way, each entry references, but does not directly contain its payload.
Each entry is stored as a UTF-8-encoded JSON object that does not contain any whitespaces or otherwise unnecessary characters, with the following attributes:
- `author` - the public key of the author that submitted the entry, as a base64 string.
- `node` - the ID of the node that the entry is being added to, as a base64 string.
- `authors` - the public keys of the authors of the entry's node, as a base64 string.
- `predecessor` (optional) - the ID of the previous entry that this entry is building on, as a base64 string.
- `type` - the entry's type, as a string.
- `signature` - a signature of the entry header, except its ID and the signature itself.

| Segment Name | Length (in Bits) | Type | Description |
| ---- | ---- | ---- | ---- |
| ID | 128 | UUID | A value that can be used to uniquely identify the entry. |
| Author | 256 | Public Key | The ID of the author that submitted the entry. |
| Node | 128 | UUID | The ID of the node that the entry is being added to. |
| Node Authors Count | 32 | Unsigned Nonzero Integer | The full number of the node's authors. |
| Node Authors | multiple of 256 | Public Keys | A complete list of all the node's authors. Its length is as specified in Node Authors Count |
| Predecessor | 128 | UUID? | Optionally, the ID of the previous entry that this one builds on. Otherwise, zero. |
| Type | 256 | String | An identifier that describes what kind of data the entry contains and what it does to the node. |
| Signature | 512 | Raw Data | A signature of the entry's entire data contents made using the submitting author's private key. |
| Size | 32 | Unsigned Integer | The unsigned length of the payload in bits. |