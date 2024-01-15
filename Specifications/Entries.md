# Entry Format
Each entry is stored and shared as a block of binary data which consists of a fixed-length header and a variable-length payload.
## Header
An entry header is a sequence of fixed-length binary data segments stringed together in a fixed order without separators.
## Payload
An entry payload is an optional blob of binary data. It can be of any length as specified in the header, including zero, and does not need to follow any specific format.