# Specifications for Block Formatting
Blocks can contain any binary data, without exceptions. No part of a Zenea Data Layer network should ever enforce any regulations regarding the type of data that blocks contain. This especially means that blocks can for example be empty, meaningless, encoded or encrypted, and that the purpose or meaning of a block's information does not need to be understood by any part of such a network. Any block can at any time be regarded as simple type-erased binary data.
### Maximum Block Length
This freedom, however, does not include the size of a block's content, as that can be critical for services storing or transmitting blocks.

A block's length, which is the amount of bits it contains, must not exceed 2<sup>16</sup> = 65536.
### Rolling Checksums
Furthermore, blocks can be split at the point of creation by so-called rolling checksums. By doing so, an amount of data bigger than a single block can be split up into several pieces based not on the maximum block length but rather on their content. When data is inserted to or removed from the collection afterwards, the blocks' boundaries do not change as often, which increases data efficiency and deduplication.

Rolling checksum boundaries should be applied whenever possible and if it does not compromise the data contained in a block.
# Specifications for Hashing Algorithms
Each block's ID is a cryptographic hash digest in hexadecimal form, accompanied by an identifier of the used algorithm.

There are a number of different hash functions in use. While the 256-bit [SHA2](https://en.wikipedia.org/wiki/SHA-2) function should be used by default, any software communicating as part of a Data Layer network should be able to handle and use the following algorithms:
- `sha2-256` (aliases `sha2_256`, `sha-256`, `sha_256`, `sha256`): The 256-bit version of the SHA2 family.
- `sha2-512` (aliases `sha2_512`, `sha-512`, `sha_512`, `sha512`): The 512-bit version of the SHA2 family.