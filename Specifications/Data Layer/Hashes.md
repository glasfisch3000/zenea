# Hashing Algorithms
Each block's ID is a cryptographic hash digest in hexadecimal form, accompanied by an identifier of the used algorithm.

There are a number of different hash functions in use. While the 256-bit [SHA2](https://en.wikipedia.org/wiki/SHA-2) function should be used by default, any software communicating as part of a Data Layer network should be able to handle and use the following algorithms:
- `sha2-256` (aliases `sha2_256`, `sha-256`, `sha_256`, `sha256`): The 256-bit version of the SHA2 family.
- `sha2-512` (aliases `sha2_512`, `sha-512`, `sha_512`, `sha512`): The 512-bit version of the SHA2 family.