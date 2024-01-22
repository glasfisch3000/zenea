# Layers
The Zenea Project consists of two layers of data transfer. The Data Layer is a simple protocol for storing and distributing blocks of data. The Node Layer builds on top of the Data Layer and utilises it to introduce a version-controlled file system that is the core of Zenea data sharing.
# Data Layer
The Zenea Data Layer packages data into so-called blocks.
A block only ever holds two sets of information:
1. Its unique **ID**, which is a hash of its content.
2. Its **content**, which is type-erased binary data of any size.
There can never be two different blocks with the same ID. Therefore, there can also never be two different blocks with the same content.
A block cannot be modified, as this would change its content and ID, making it an entirely new block independent from the old one.
Blocks can be freely distributed among members of a Data Layer network, as their is no such thing as author- or ownership. The integrity of any block's data can always be verified by hashing its contents and comparing the result to its ID.
# Node Layer
The Zenea Node Layer builds on top of the Data Layer. Its use requires the underlying system of distributing hash-identified blocks of data.
The Node Layer introduces several abstract concepts as described below to build a system of version-controlled data structuring.
## Nodes
The very basis of Node Layer data storage and sharing are nodes. A node is itself an abstract concept, a container whose main and only point of interest is the information associated with it, comparable to a traditional file system directory, a chatroom or a bulletin board. Other than with file systems, however, there is no central registry of any kind. A node only ever exists implicitly in the form of atomic pieces of data referencing it that are called *entries*.
A node is owned by one or more *authors*.
Each node is uniquely identified by:
- an **ID**.
- its [authors](#Authorship) (their **public keys**).
## Entries
Entries are the atomic units of data that are used to package all information that is sent and stored using the Zenea protocol. An entry can, depending on its type, represent any piece of data, like a message or comment, a git commit or a blog post.
Each entry contains:
- a unique **ID**.
- a **timestamp** of when the entry was submitted.
- a [node's](#Nodes) **ID and authors**.
- optionally, the identifier of the **previous entry** it builds on.
- the **public key** of a singular [author](#Authorship) that submits and signs the entry.
- a **type identifier** that describes what kind of data the entry contains and what it does to the node.
- optionally, a **payload** that can be data of any kind or size.
All the attributes of an entry except the payload are together called an **entry header**.
## Versions
Each entry can optionally point to exactly other previous entry. In this way, a collection of entries all referencing the same node form one or more *version trees* of that node. Such a tree consists of vertices that are entries where each vertex points to its parent. An entry that does not point to another entry is the root of a new version tree.
Any subtree starting at the root of a version tree is a sequential list of consecutive entries all referencing the same node where the first one does not point to any other entry. Such a list of entries can be interpreted to form a final set of data known as a *version* of the referenced node.
The way these entries are interpreted depends on the client, however there should always be one generally accepted way of doing so. This necessitates general specifications on how to process any type of entry and the data it contains.
# Authorship
An author is an entity who owns or partially owns a node. Like a node itself, an author is an abstract concept that does not hold any data and is not stored anywhere. An author simply exists in the form of its identification which is a public cryptographic key.
## Security and Verification
An entry always refers to a node which is owned by one or more authors and may therefore add to or change the data that they own. Additionally, when collaborating on a set of data, it is often useful to know who exactly has made a particular change. This necessitates a form of authorship security, where any entry's author is known at all times and can especially be verified by anyone to be or not be an owner of the node in question.
Zenea achieves such security using asymmetric cryptography. Each author entity consists of a cryptographic key pair:
- The private key is stored safely in a location only accessible to the author.
- The public key is used as the author's identification and therefore accessible to the public.
Each entry must contain an author's identification (which is their public key) and have its entire contents signed using that author's private key. This signature can be verified by anyone using the public key. Viewers of a node may process an entry submitted to that node differently based on whether or not its author is one of the node's owners.
