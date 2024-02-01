# Data Structuring
## Nodes
The very base of Zenea data storage and sharing are nodes. A node is itself an abstract concept, a container whose main and only point of interest is the information associated with it, comparable to a computer file folder, a chatroom or a bulletin board. Other than with traditional file systems, however, there is no central registry of any kind for nodes. A node only ever exists implicitly in the form of atomic pieces of data associated with it that are called *entries*.

A node is owned by one or more *authors*.

Each node is uniquely identified by:
- an **identifier**.
- its [authors](#Authorship) (their **public keys**).

## Entries
Entries are the atomic units of data that are used to package all information that is sent and stored using the Zenea protocol. An entry can, depending on its type, represent any piece of data, like a message or comment, a git commit or a blog post.

Each entry contains:
- a [node](#Nodes) (its **identifier and authors**).
- optionally, the previous entry it builds on (its **identifier**).
- a singular [author](#Authorship) that submits and signs the entry (their **public key**).
- a unique **identifier**.
- a **type identifier** that describes what the entry does to the node.
- optionally, a **payload** that can be data of any kind or size.

## Versions
Each entry can optionally point to exactly other previous entry.
In this way, a collection of entries all referencing the same node form one or more *version trees* of that node. Such a tree consists of vertices that are entries where each vertex points to its parent. An entry that does not point to another entry is the root of a new version tree.

Any subtree starting at the root of a version tree is a sequential list of consecutive entries all referencing the same node where the first one does not point to any other entry. Such a list of entries can be aggregated and interpreted in any way to form a final set of data known as a *version* of the referenced node.

For each possible version of any node, there should be one generally accepted way of interpreting it. This necessitates general specifications on how to interpret any type of entry and the data it contains.

# Authorship
An author is an entity who owns or partially owns a node.

Like a node itself, an author is an abstract concept that does not hold any data and is not stored anywhere. Each author simply exists in the form of its identification which is a public encryption key.
## Security and Verification
An entry always refers to a node which is owned by one or more authors and may therefore add to or change the data that they own. At the same time, when collaborating on a document, it is often useful to know who exactly has made a particular change.
This necessitates a form of authorship security, where any entry's author is known at all times and can especially be verified by anyone to be or not be an owner of the node in question.

Zenea achieves such security using asymmetric encryption. Each author entity consists of an asymmetric encryption key pair:
- The private key is stored safely in a location only accessible to the author.
- The public key is used as the author's identification and therefore accessible to the public.

Each entry must contain an author's identification (which is their public key) and have its entire contents signed using that author's private key. This signature can be verified by anyone using the author's public key.
Viewers of a node may process an entry submitted to that node differently based on whether or not its author is one of the node's owners.
