
 blocks are filled with standard Ethereum transactions. After the Cancun-Deneb fork, blocks can be filled with a combination of these typical Ethereum transactions, and so-called blob-carrying transactions.

blob-binary large object 
Blobs can be imagined as ‘side-cars’ full of data that will ride alongside blocks. The transactions that fill Ethereum blocks don’t necessarily have to have blobs riding with them, but a blob cannot be included in the network without an associated blob-carrying transaction making its way into a block. While exactly how blobs will be used (and by whom) remains to be seen, it is assumed that the sequencers of Ethereum Layer 2 rollups will be the primary consumer of ‘blobspace’, and that blobs will primarily contain batched transactions that were executed on these rollups. Moreover, we can think of these blobs as ‘compressed’ data structures, like a .zip file.

 the blob-carrying transaction doesn’t actually include the blob data; only a reference to it in the _blob_versioned_hashes_ field (item 2 above). Technically, this reference is a hash of a [KZG commitment](https://dankradfeist.de/ethereum/2020/06/16/kate-polynomial-commitments.html) to the blob, but for our purposes, it's sufficient to think of this as a fingerprint that is unique to each blob and that can be used to tie each blob to a blob-carrying transaction.

https://notes.ethereum.org/@vbuterin/blob_transactions_simple
https://notes.ethereum.org/@vbuterin/blob_transactions

The execution will only happen on the Beacon Chain for the purposes of rollups (fraud proofs and validity proofs) and then validators assigned to random shards will only be in charge of serving rollup’s data to whoever asks for it.


