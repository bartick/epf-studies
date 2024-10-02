## Block time

Block time refers to the time separating blocks. In Ethereum, time is divided up into twelve second units called 'slots'. In each slot a single validator is selected to propose a block. Assuming all validators are online and fully functional there will be a block in every slot, meaning the block time is 12s. However, occasionally validators might be offline when called to propose a block, meaning slots can sometimes go empty.

## Block size

Blocks themselves are bounded in size. Each block has a target size of 15 million gas but the size of blocks will increase or decrease in accordance with network demands, up until the block limit of 30 million gas (2x target block size). The block gas limit can be adjusted upwards or downwards by a factor of 1/1024 from the previous block's gas limit. As a result, validators can change the block gas limit through consensus. 
The total amount of gas expended by all transactions in the block must be less than the block gas limit. 
This is important because it ensures that blocks can’t be arbitrarily large. If blocks could be arbitrarily large, then less performant full nodes would gradually stop being able to keep up with the network due to space and speed requirements. The larger the block, the greater the computing power required to process them in time for the next slot. 
This is a centralizing force, which is resisted by capping block sizes.
