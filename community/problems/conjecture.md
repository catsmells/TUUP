# How Does True Decentralization Allow for Everyone to Speak Fairly?

During the creation of a blockchain project I was working on, an interesting issue seemed to arise. After refining the structure of the problem, and after considering 
possible solutions (that led to nowhere) I figured I should e-mail different university computer science departments to see if they had an answer. After getting ignored 
multiple times, I went to a few STEM-centric message boards & chats. Nobody could seem to figure out a solution, and for the time being I'm completely stumped here.

***The Scenario:*** Consider a basic blockchain network. This is a gasless protocol, where a user may create a wallet on-chain. The wallet will allow them to purchase/mint
NFTs as need be, but it is required they have a wallet [address] to do so. This is an absolutely non-KYC, privacy-centric network. When a new user (wallet) is created on-chain,
the network creates an NFT representing the user on the network. To be clear:

- Layer 0: The Concept
- Layer 1: The Protocol
- Layer 2: The Network
- Layer 3: The Application

To account for the possibility of as many users as possible, it is highly recommended to allow for an infinite amount of user tokens (wallet tokens) to be created. Multiple users
are allowed to create multiple wallets, as developers and high-frequency traders are expected to do so.

As it currently stands, there is a sort of "queue" for wallet token creation. If multiple users choose to create wallets on-chain, it would be first come, first serve. The processing
ability of this protocol is well-crafted; multiple user wallet creations would be practically instant. If one were to choose to create a near-infinite maximum bound for a "v1" protocol
and create a system of matching keys from a limited pseudorandom set, that may also work. 

***The Challenge:*** Prevent a denial-of-service attack from occurring with wallet token creation. To be clear: 

1. If you choose to go the limited large number route, create a way that would prevent a bad actor from creating a large queue of private keys, matching to the already-decided public key
   amount without using a variety of "gas" or fee system.
2. If you choose to go the infinite token route, create a method of mathematical (or logical) friction that would prevent a bad actor from queuing hundreds of millions of new wallet minting requests.

If you believe there isn't a solution to this, prove that a solution cannot be made.
