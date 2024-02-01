# Block Contents
Blocks can contain any binary data, without exceptions. No part of a Zenea Data Layer network should ever enforce any regulations regarding the type of data that blocks contain. This especially means that blocks can for example be empty, meaningless, encoded or encrypted, and that the purpose or meaning of a block's information does not need to be understood by any part of such a network. Any block can at any time be regarded as simple type-erased binary data.
# Block Size
The freedom of content, however, does not include a block's size, as that can be critical for services storing or transmitting blocks.

Any block's length, which is the amount of bits it contains, must not exceed 2<sup>16</sup> = 65536.
### Rolling Checksums
Furthermore, blocks can be split at the point of creation by so-called rolling checksums. By doing so, an amount of data bigger than a single block can be split up into several pieces based not on the maximum block length but rather on their content. When data is inserted to or removed from the collection afterwards, the blocks' boundaries do not change as often, which increases data efficiency and deduplication.

Rolling checksum boundaries should be applied whenever possible if it does not compromise the data contained in a block.