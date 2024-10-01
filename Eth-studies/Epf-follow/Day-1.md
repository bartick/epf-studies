i just started with the wiki 
trying to sort things out and put everything into order

## Merkle trees 
**Merkle tree** is a [tree](https://en.wikipedia.org/wiki/Tree_(data_structure) "Tree (data structure)") in which every "leaf" [node](https://en.wikipedia.org/wiki/Tree_(data_structure)#Terminology "Tree (data structure)") is labelled with the [cryptographic hash](https://en.wikipedia.org/wiki/Cryptographic_hash_function "Cryptographic hash function") of a data block, and every node that is not a leaf (called a _branch_, _inner node_, or _inode_) is labelled with the cryptographic hash of the labels of its child nodes. A hash tree allows efficient and secure verification of the contents of a large [data structure](https://en.wikipedia.org/wiki/Data_structure "Data structure"). A hash tree is a generalization of a [hash list](https://en.wikipedia.org/wiki/Hash_list "Hash list") and a [hash chain](https://en.wikipedia.org/wiki/Hash_chain "Hash chain").
- https://www.youtube.com/watch?v=V6gLY-1G4Mc
- 
## Commitment scheme

A **commitment scheme** is a [cryptographic primitive](https://en.wikipedia.org/wiki/Cryptographic_primitive "Cryptographic primitive") that allows one to commit to a chosen value (or chosen statement) while keeping it hidden to others, with the ability to reveal the committed value later.[[1]](https://en.wikipedia.org/wiki/Commitment_scheme#cite_note-Goldreich-1) Commitment schemes are designed so that a party cannot change the value or statement after they have committed to it: that is, commitment schemes are _binding_. Commitment schemes have important applications in a number of [cryptographic protocols](https://en.wikipedia.org/wiki/Cryptographic_protocol "Cryptographic protocol") including secure coin flipping, [zero-knowledge proofs](https://en.wikipedia.org/wiki/Zero-knowledge_proof "Zero-knowledge proof"), and [secure computation](https://en.wikipedia.org/wiki/Secure_computation "Secure computation").


It serves two main properties:

1. **Hiding**: The commitment does not reveal the committed value. The receiver cannot determine the value just by looking at the commitment.
2. **Binding**: Once the committer has made a commitment, they cannot change the value without being detected. This ensures that the committer cannot "cheat" by claiming they committed to a different value.


commitment is based on **modular arithmetic** and **hashing**

### **Hash-based Commitment Scheme**

#### Components:

- Let H(x)H(x)H(x) be a cryptographic hash function (like SHA-256), which takes an input xxx and produces a fixed-length output.
- mmm is the message (value) that the committer wants to commit to.
- rrr is a random value (often called a "nonce" or "salt") that is chosen by the committer to ensure hiding.

#### Commitment Process:

- The committer computes a commitment as:
    
    C=H(m∣∣r)C = H(m || r)C=H(m∣∣r)
    
    where ∣∣||∣∣ denotes concatenation, and CCC is the commitment.
    
- The committer sends CCC (the commitment) to the receiver but keeps mmm and rrr secret.

#### Reveal Process:

- To reveal, the committer sends both mmm and rrr to the receiver.
- The receiver verifies the commitment by computing H(m∣∣r)H(m || r)H(m∣∣r) and checking if it matches the original CCC


Now ill look into the ethereum dev docs https://ethereum.org/en/developers/docs at least the foundational topics (revisor) 

-https://summerofprotocols.com/wp-content/uploads/2023/12/53-BEIKO-001-2023-12-13.pdf