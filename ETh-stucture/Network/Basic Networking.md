
# EL
The execution layer's networking protocols is divided into two stacks:

- the discovery stack: built on top of UDP and allows a new node to find peers to connect to
    
- the DevP2P stack: sits on top of TCP and enables nodes to exchange information
    

Both stacks work in parallel. The discovery stack feeds new network participants into the network, and the DevP2P stack enables their interactions.

### Discovery

Discovery is the process of finding other nodes in network. This is bootstrapped using a small set of bootnodes

## The consensus layer

The consensus clients participate in a separate peer-to-peer network with a different specification. Consensus clients need to participate in block gossip so that they can receive new blocks from peers and broadcast them when it is their turn to be block proposer. Similar to the execution layer, this first requires a discovery protocol so that a node can find peers and establish secure sessions for exchanging blocks, attestations etc.

![[nework.png]]
