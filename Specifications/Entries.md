# Entry Format
Each entry is stored and shared as a block of binary data. It consists of an **entry header** made up of fixed-length segments in a fixed order and an **entry payload** that can be of any length, including zero, as specified in the header.

| Segment Name | Length (in Bits) | Type | Description |
| ---- | ---- | ---- | ---- |
| ID | 128 | UUID | A value that can be used to uniquely identify the entry. |
| Author | 256 | Public Key | The ID of the author that submitted the entry. |
| Node | 128 | UUID | The ID of the node that the entry is being added to. |
| Predecessor | 128 | UUID? | Optionally, the ID of the previous entry that this one builds on. Otherwise, zero. |
| Type | 256 | String | An identifier that describes what kind of data the entry contains and what it does to the node. |
| Signature | 512 | Raw Data | A signature of the entry's entire data contents made using the submitting author's private key. |
| Size | 32 | Unsigned Integer | The unsigned length of the payload in bits. |