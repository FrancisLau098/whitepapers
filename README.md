Skycoin: A New System for Distributed Consensus
===========

Abstract: 
A new cryptographic primitive known as a public broadcast channel is introduced. A new consensus algorithm implementation, Obelisk and new coin Skycoin built upon Obelisk are introduced. Obelisk is not a single algorithm, but an implementation employing multiple techniques to deliver specific security guarantees.


Bitcoin
=======
Overview Of Bitcoin as a solution to the byzantine generals problem. 

New transactions are placed into a block, which is appended to the blockchain. Any peer in the Bitcoin network can create new blocks. Each block therefore has a single parent but one or more valid successors (children).  The chains form a tree and the core problem of Bitcoin solves is getting every node in the network to agree on which which of prospective chains in the chaintree is the consensus blockchain.

Bitcoin uses a technique called Proof-of-Work to determine a unique blockchain. A valid block requires a hash value which is below a target value. Nodes add transactions to a new block and randomly try notches until a valid hash for a block is found.

A function is used to create a total ordering of chains in the blocktree. The chain which has the highest difficulty and required the most hashing operations to produce is "the longest chain" and consensus chain. The notion of "block depth" and "difficulty" create a total ordering over all linear chains in the blocktree and we accept the most resource intensive to produce chain as the consensus chain.

Bitcoin nodes connect to each other randomly and each node relays the most difficult chain of blocks that it knows about to its peers. If one node has a more difficult to produce chain than another connected peer, the peer will receive the blocks sequentially. The peer will evaluate the function and decide that received chain is more difficult to produce and therefore switch its consensus to the received chain. The peer will then advertise its new chain to its peers. In this way, consensus is propagated throughout the network and all nodes reach the same consensus.

Bitcoin does not assume that nodes have identities and does not assume that nodes are honest. Nodes may send other nodes any data and it cannot affect consensus decisions, because difficulty is something that can be independently verified on its own merit.


Innovation in Bitcoin
====

Bitcoin has made several innovations that need to be kept in mind:
- a single datastructure that everyone has a copy of (the blockchain)
- storing financial transactions in the blockchain (public ledger for transactions)
- use of PoW and difficulty retargeting to maintain a constant rate of block production
- use of public key hashes as addresses (public keys are not disclosed until used)
- use of "outputs" for balances. Ignores trying to create divisible digital cash: To pay $20 from a $25 output, send $20 to person and $5 back to yourself.
- first use of function (PoW difficulty function and block depth) to define total ordering on block trees
- public ledger circumvents double spending problem in traditional digital cash

Flaws in the Bitcoin System
============================

The Bitcoin system suffers from these flaws:

- Consensus decisions in Bitcoin are not final and can be reverted. A person or organization who can rent or buy enough hashing power can revert transactions.
- Bitcoin achieves network consensus but individual Bitcoin nodes are highly vulnerable to adversaries who control the routers through which packets pass. A router controlling adversary has absolute control over the view of a node of the network and can arbitrarily influence the nodes consensus decisions: Attacking a Bitcoin node used by a bank to execute a double spending attack is easier than attacking the whole network to do a double spending attack.
- The security of the Bitcoin network depends upon the cost to achieve majority hash rate being too great for an individual or organization that would attack the network. This is not a valid assumption. As Bitcoin grows in success and value, the incentives to attack the network have increased. 
- Successful attacks can steal incredible sums from exchanges ($400 million in the most recent MtGox attack). An skilled attacker can buy alt coins from an exchange in Bitcoin and then 51% attacks to revert the Bitcoin deposit transaction. The user now has both the Bitcoin and the alt coins and the exchange is insolvent because of liabilities to depositors that cannot be met.
- Attackers can steal substantial sums from banks and gambling sites. An attacker deposits Bitcoin and then withdraws it. The attacker uses a 51% attack to revert the deposit transaction, while keeping the withdraw transaction. Such an attack is likely to come suddenly, be extremely profitable and affect all Bitcoin operating services, who are not fortified against the possibility.
- As Bitcoin matures, criminals can gain massively by buying options against Bitcoin and attacking the network. In the future, successful attacks on Bitcoin could result in several hundred millions of dollars in profit from options trading. 
- The cost to achieve majority hash rate may not be high enough to protect against a dedicated attacker. KNC miner has shipped batches of 200 units for $10,000 each, which together achieved majority hashrate. The cost to attack the Bitcoin network is therefore less than 2 million dollars.
- The cost to attack the Bitcoin network is within the resources of nation states and corporations who may attempt to discredit the security of Bitcoin. Countries with strong capital controls and competing corporations may directly attack the Bitcoin network to protect their financial interests.
- Services which allow "cloud hashing" and rental of 3rd party hash power are increasingly successful. Many large pools now have the ability to rent the hash power for a majority attack.
- Hackers can use numerous security holes in routers and networking equipment to steal coins from banks and exchanges. An attacker can control the peers a Bitcoin node is connected to and ensure connections to attacker controlled nodes. An attacker may introduce a deposit transaction to the side chain of a bank and get the bank to issue a withdraw transaction which is then relayed to the main network. 
- Bitcoin cannot offer security at a low cost. The cost to run the Bitcoin network is extremely high. The Bitcoin network is using immense and exponentially growing amounts of electricity and is environmentally irresponsible. Bitcoin's security purposely relies upon creating as much electrical waste as possible. A secure system costs more to attack than defend. In a well designed system, $1 in security costs $1000 to circumvent. In Bitcoin the ratio is $1 to $1.
- Bitcoin transactions take on average 10 minutes to get included in a block, and more time is required for more security. Bitcoin fundamentally cannot decrease transaction times without compromising security. This hinders Bitcoin adaption at the point of sale.

These are the issues that must be addressed. In light of these issues, Bitcoin should be regarded as embryonic, but not final form of cryptocurrencies. Future currencies will improve significantly on Bitcoin and surpass it in many ways.

Desirable Properties For Systems of Distributed Consensus for Financial Ledgers
==========

The criteria on which Bitcoin can be improved are:
1. Security
2. Efficiency
3. Speed
4. Transparency

1. Once a transaction has executed, it should be impossible to revert consensus. Consensus should be irreversible as possible. (no double spending, security)
2. The cost to run a perfectly secure ledger should be extremely low. (efficiency)
3. The system should allow transactions to be confirmed within seconds (speed)
4. It should be easy to audit and identify malicious nodes (transparency)
5. Nodes should be able to detect if their consensus differs from the network (router attack, security)
6. Some security properties should remain intact even if the vast majority of nodes in the network are malicious and colluding

We introduce a system called Obelisk which achieves these objectives.

Byzantine Generals Problem In The Real World
======


The Byzantine Generals Problem is a model used by academics for designing algorithms that allow networks of computers to come to an agreement. A successful consensus algorithm requires all of the honest nodes to come to the same agreement.

In the Byzantine Generals Problem, you have N generals sieging a city. The generals can only communicate over faulty communication channels and all must come to the same decision. They must all attack on the same day. To conquer the city, all the generals must either attack or stay put. If one general attacks, all the generals should attack and if one waits, all generals should wait. If one general attacks and the other generals stay put, the siege fails. The generals can only communicate by letter and the letters may not arrive or may arrive late. 

In the academic version of the Byzantine Generals Problem, the failures are benign. Maybe a general does not get a letter. The represents faulty but benign computer servers which should all come to the same state. The real world Byzantine Generals Problem is called the "Adversarial Byzantine Generals Problem". The Adversarial Byzantine Generals problem is what happens when someone has a financial incentive to attack the network.

There are dishonest generals and they will do everything possible to ensure that consensus fails. Dishonest generals can lie. They can tell one general one thing and another something else. Dishonest generals can kill the messenger of another general so that a message sent is not received. Dishonest generals can forge messages from other generals. Dishonest generals can change the message an honest general sent. The dishonest generals can collude.

In Bitcoin, they will go even further and engage in bribery and hacking. They will hunt down your employees and hack into the computers of contractors to gain access to your servers. They will manipulate system clocks, compromise routers, use hash collisions, flood the network with hundreds of thousands of bots and exploit signature malleability.

A secure system must not only protect against every known attack, but be robust enough to evolve and survive all future attacks. Some issues in Bitcoin can be fixed, such as signature malleability. Other issues are fundamental and cannot be addressed without defining an entirely new framework, such as the reliance on Proof of Work and miners.

Skycoin Security Philosophy:
========

Security is a process of continuous identification and fortification against threats. A good system achieves "defense in depth", has multiple redundant systems and will survive the complete failure of any individual measure. 

Good security comes not from the paranoia of protecting against every possible imaginable threat, but upon knowing which threats are existential and which are mere annoyances. 

Good security achieves a multiplier effect. A dollar that costs an attacker ten dollars in resources to steal is a dollar that is safe.

No single system could achieve all of the objectives a successor to Bitcoin requires. Skycoin instead takes a modular layered approach and uses different systems to enforce particular guarantees. Skycoin was designed as a fortress with multiple layers of overlapping defense. 

Skycoin security is focused on protecting against the existential threats to Bitcoin and the daily threats that day to day users face. Skycoin security attempts to give the highest degree of protection against the class of attacks that would inflict the greatest loses upon its users, stakeholders and institutions. This required a complete redesign of Bitcoin at both ends from wallet generation to blockchain consensus. It requires a vision of what we are trying to achieve and requires fundamental innovation in several areas to get there.

Most of the losses in Bitcoin have been from oversights in design, lack of usability and at the end user rather than fundamental technical attacks on the software or mathematics. A user backs up his wallet, makes some transactions and reformats his computer. He thinks his coins are safe because he has a wallet backup (unlike his stupid friend who lost hundreds of thousands of dollars in Bitcoin because they forgot to make backups). He loads the wallet and half his coins are missing. Bitcoin generates new addresses and sends coins to those addresses as change every transactions, but the new addresses are not in the wallet backup because they were not generated at the time the backup was made.

Skycoin must address both the looming existential mathematical threats while addressing the security perils that Bitcoin's incomplete and poorly thought out user experience has created for everyday users. The poor usability and design has forced users to compromise security and even paranoid power users with millions of dollar routinely rely on insecure web wallets. Despite the frequent and massive thefts reported by the media on a daily basis, to date more Bitcoin have been lost to usability issues than all the efforts of criminals to steal Bitcoin.

As many as half of the total existing Bitcoin have never been moved from their initial addresses and never will be. They are simply lost. Unrecoverable wallet files, lost wallets, misunderstandings of what was actually being backed up in a wallet file. MtGox recently reporting "finding" 200,000 Bitcoin in a wallet they didn't know had Bitcoin in it. The wallet was ignored and easily could have been deleted under the mistake it had no coins in it (which has happened to many) because the software was unable to load the wallet because it was "too old". 

Most of the security issues are at that level. They are about usability, end users and exchange security. The rest of this paper is covers some of the new techniques we have created to address network level security and secure the Skycoin blockchain.

We have proven mathematically that our system achieves consensus, has the security properties we want and operates well under normal network conditions. We have some exciting new data-structures that have not been seen in any coin or piece of software before. Now we are prototyping the system for deployment.  The Skycoin development process is iterative. There will be changes, improvements and refinements as we work through the details, address known flaws, test the system and get feedback.


Public Broadcast Channels: Personal Blockchains
==========

In Adversarial Byzantine Generals Problem there are several communication assumptions
- messages may arrive out of order
- messages may not arrive
- dishonest generals may say one thing to one person and another thing to another
- dishonest generals may lie
- dishonest generals may forge signatures of other generals
- dishonest generals may intercept and modify messages from other generals

We introduce a new cryptographic primitive called a public broadcast channel and describe its implementation. This primitive has the following properties
- you cannot say one thing to A and another thing to B 
- the communication is public
- the communication could not have come from anyone but you (authenticated)
- once publish something, it cannot be easily unpublished
- you cannot backdate a communication without being detected (linked timestamping/hash chain)
- the messages arrive in order
- the message cannot be modified in transmission

The public broadcast channel is implemented as a block chain. Everyone can read the chain, but only the owner can mint blocks for it. To be valid for a personal chain, each block must be signed by the owners private key. 

Each Obelisk node has a personal blockchain and it is the core primitive in the Obelisk system.

The public broadcast channel imposes several constraints
- Once a block is published, it cannot be unpublished (blocks are replicated peer to peer to all subscribers. Once a block has been published, it spreads to all subscribers. You have to destroy all peers who have received the block to erase it from internet).
- A node cannot publish a different version of an earlier block without detection (blocks are numbered and it would be detected if the node signed two different blocks with the same sequence number)
- A node cannot backdate the time stamp on the receipt of a block, without delaying the publication of a block (timestamps only go up, time stamps increase monotonously with block sequence count)
- A block in the middle of the chain cannot be changed without invalidating every block that comes after it (hashchain, each block header contains a hash of the previous block)


Obelisk: 
=======

Each Obelisk node (Skycoin Consensus Node) has a public key (an identity) and personal blockchain (a public broadcast channel). Consensus decisions and communication happen within the personal blockchains of each Obelisk node. This is a public record of everything a node does. This allows the community to audit nodes for cheating and collusion. It gives the community a way identify nodes which are participating in attacks on the network and it makes public how decisions in the network are being made and which nodes are influencing those decisions.

Each node has a list of other nodes that it subscribes to. Nodes with more subscribers are more "trusted" and yield more influence in the network. If the community does not trust the nodes representing them or feels that power within the network is too concentrated (or not concentrated enough) the community is able to collectively shift the balance of power in the network by collectively changing their trust relationships in the network.

Node subscription relationships can be random and/or can be formed through web of trust (subscribe to nodes of people you know and people in community you trust).

When a node receives a new block from a chain it is subscribed to, it publishes the hash of the block it publishes. This is a public acknowledgment of the receipt of the block. Each block is timestamped and counter references blocks from other chains. This creates a dense interlinked chains of block acknowledgments. These chains establish causal relationships and can act as a distributed time stamping system as described in the next section. This allows the network to prove that data did not exist or was not published to the network or establish that particular nodes were active or offline during a particular time interval.

The current Obelisk consensus algorithm is based upon Ben-Or's randomized consensus algorithm.

A Sybil attack in a random graph (worse case) allows the Sybil nodes to control consensus, but the nodes are unable to revert transactions, removing the only economic incentive to attack the network. In real world graphs the Sybil resistance of the network is actually very high and running a node is moderately costly in terms of bandwidth, which make large botnets prohibitive.

Trust relationships are scarce and can be rescinded. In the event of an attack, the network reacts by severing connections to less trustworthy nodes and contracting to a smaller core of trusted nodes. The public record left by each node's personal blockchain makes it very easy to identify the nodes participating in an attack. As attacking nodes are identified individuals sever relationships with those nodes, reducing their influence.


- Skycoin consensus is democratic and nodes are run by the community. 
- Skycoin node consensus is public
- Every node is accountable to the community and 3rd party audits.
- Influence within the Skycoin consensus system is democratic and transparent (but unequal).

Simple Binary Consensus Algorithm: Choosing between two blocks
====

Each voting decision is a hash pair (A,B). A is the hash of the parent of the block and B is the hash of the block.

Each node votes on the next block it believes should be the consensus block. If 40% of the nodes it is subscribed to have the same candidate for consensus, the node changes its consensus to that block. The node flips randomly between candidates until consensus is reached.

Consensus on Multiple Concurrent Branch Choices:
====

A more advanced system publishes (A,B, P) Where P is value from 0 to 1. P values across all successors to block would sum to 1. This allows for concurrent consensus decisions on multiple chain branches.

If the majority of nodes in the network are honest, they will also converge to the same consensus.

Skycoin also has a limited form of Proof of Stake. We bias voting in favor of blocks with a larger transaction fee.

If there are only two possible consensus choices for given parent and both blocks execute your transaction, then the transaction is effectively executed regardless of which of the two blocks end up chosen by the network.

The probability of reversion of an early consensus decision declines exponentially with block depth.


Advanced Topics in Consensus
====

By constructing the network link adjacency matrix, we can compute the Eigenvalue centrality measure which measures the influence of each node. We can cluster the graph and find the influential subclusters of nodes and then sampling nodes from the subclusters can determine if global consensus has been reached.

The efficiency of the algorithm declines with the number of blocks the network has to choose from in each round. We may use Proof of Work, with no reward and difficulty retarget as a throttle rate on the introduction of new candidate blocks.

If we could guarantee a single block per decision period, consensus becomes trivial. We can achieve this by imposing a total ordering on the blocks in the consensus round and dropping all but the top. Example: the block with the largest transaction fee that was published within fifteen seconds of the last block. There is no way to do an exact, fair, distributed time stamp everyone will agree one, but any way to construct a total ordering would work.

Another method uses a "fair" block lottery to choose the node that will mint the next block. It has to exploit the graph structure so trusted people and not sybil atack nodes get the block minting rights. Its easy to construct if you have the global graph and replicate all chains for each node, but very difficult using only local information available to each node.

In another scheme, you use the consensus to vote a committee of nodes to mint block. The right to mint the next block passes around in circles over a list of elected nodes. Once the system in place, you can try different things. Nodes can be programmed to communicate and act autonomously. People can update their node's program to automatically kick deadbeats off the elected board of block minters. If enough nodes added that script, it would become an enforced rule.

The personal blockchains act as ballots with scriptable behavior. Individuals can add scripts to their node for detecting bad nodes and severing relationships with them. The network can acquire attack immunity locally, through the actions of individual users choosing the scripts to run on their node instead of from a central patch by the developers.

We are at an early stage of understanding what is possible with personal blockchains.

Attack Types:

===

There are four types of attacks
- dominating decisions on block consensus (potential denial of service)
- reverting consensus which had previously become unanimous (double spending)
- delaying consensus (denial of service)
- attacking individual nodes by controlling their view of the network

An adversary who controls the majority of the influence in the network controls the consensus decisions of the network. However, they are unable to easily double spend or 51% attack. A adversary which controls the network can vote for blocks that contain no transactions and other annoyances. Such behavior is easily detected (public behavior) and nodes easily banned if they become disruptive.

To revert consensus, requires a majority of nodes to be hostile and collude. The malicious majority must go offline, allow the main network to reach a particular consensus and then resume communication with the rest of the network. Any node which whose connections consist of a majority of attacking nodes will be successfully recruited in the 51% attack (in the naive version). However, If the attacking nodes are less than a majority, the effort will fail.

This is the only way to revert transactions. This is the only attack and is extremely easy to detect. Trustworthy nodes quickly sever relationships with attacking nodes. Subgraphs involved in the attack are likely to be densely connected and do not influence the network as much as more tightly integrated subgraphs. It is not enough to have a simple majority of nodes, to revert consensus an adversary much control nodes which control a majority of scarce subscription and trust relationships. Sybil attack bots have difficulty networking into a human web of trust network.

In web of trust graphs, influence is highly concentrated with nodes trusted by the community and controlled by Skycoin stakeholders. It is extremely unlikely a majority of trusted community members and institutions would benefit from, or even be able to organize a successfull majority influence attack. Community members participating are publicly identifiable and would suffer severe trust penalities for being associated with an attack attempt.

Despite the difficulty of double spending under Skycoin, it is possible to prevent the attack entirely through two separate methods. The first method severely restricts the way voting decisions are made, to greatly increase the difficulty of collusion between nodes. The second way uses distributed time stamping to identify attack nodes .

Subverting Individual Bitcoin Nodes: Easier Than Attacking Network
====

Individual Bitcoin nodes suffers vulnability to attacker who controling the network router. Such an attack can inject reset packets and control who the node can connect to. Victims can be setup for a double spending attack and coins stolen by forking the blockchain of indivial node without needing to attack the Bitcoin network. As the price of Bitcoin rises, these attacks become more likely and profitable.

Skycoin introduces a "consensus oracle" to protect banks and exchanges from targeted attacked on individual nodes. The Skycoin consensus oracle verifies an individual node is in sync with global network. The Skycoin consensus oracle takes a list of public keys of user chosen trusted nodes and verifies against the list. Discrepancy result in an alert prompting human action and safeguard measures such as suspending exchange withdrawls before funds can be stolen.


Publicly Verifiable Trusted Computing with Communicating Distributed Deterministic State Machines:
=====

We describe a system, were each node performs a computation in public. The computationa can be verified and replicated by any third party. This system consists of deterministic state machines communicating over a public broadcast channel (private blockchains).

Consensus decisions published in the block chain become outputs of a deterministic state machine, whose inputs are public data. We require that the output published in a blockchain by a node, are a deterministic function of the block data published by the nodes subscribed to. Any third party can download the public inputs to a node and verify that the output matches exactly the output (the block ) produced and published by the node. 

This approached was developed for and heavily influenced by research into adversarial Paxos. We call the implementation of Paxos on a public broadcast channel "Public Paxos".

A third party auditor can produce a mathematical proof which can be indepedently verified by third parties, proving cheating by a dishonest node. Such cheating becomes bannable and results in automatic revocation of trust relationships. The node would be severed from the network by honest nodes and unable to influence voting decisions.

A practical implementation of this system, requires 
- the implementation of a state machine or well defined virtual machine
- requires that each block contain a hash of the list of peers the node has trust relationships with
- requires a hash of the program that the state machine is running, which determines its output (block produced)
- requires publication of hash of blocks received from peers in the feed

We augment the personal blockchain with a datastructure containing some rarely changing fixed information, including the state machine's subscription list and program source code. The node publishes the hash of it subscription list and virtual machine source code in each block and publishes the subscription list and program source.

Example:

Node A is subscribed to the private chains of Node B and Node C. B mints block B1. A receives B1. A publishes a block, which includes the hash of B1 to signify the receipt of the data. The block produced by A, A1 is a deterministic function of B1.  C publishes block C1. A publishes block A1, which include a hash of block C1 it its block acknowledgement list. A2 produces and publishes and signs block A2, which must be a deterministic function of B1,C1.

Note:
- all inputs are public and available to 3rd parties (information published in a public broadcast channel)
- outputs produced by each node are deterministic functions of public input
- any 3rd party can download the same data, run the same program and generate the same output as the node itself
- the state of the machine, which generates the output might be a queue of the last 1024 blocks acknowledge by the node

Overview:
- you have N state machines
- each state machine communicates over a public broadcast channel
- the state of each machine is a queue of received messages from other state machines
- each state machine when invoked produces an output block published into the machines public broadcast channel
- the output block contains hashes (receipts) of received messages and data
- the output block is a deterministic function of the queue of received messages over the last N blocks, for finite N

In this system, nodes are highly constrained. The only leeway nodes receive is twiddling the order that messages are acknowledged. The types of attacks a node can partipate in without detection is severely limited.

Thoughts on Distributed Time Stamping:
====

The simplest time stamping service is a trusted central server with a known public key and an accurate clock. The server receives hashes and produces a signed timestamp of the hash with its private key. If the server can be trusted, the signed timestamp can be used to prove that data existed at a particular time.

Accurate, trusted digital time stamps have many applications. They can be used to determine if a node was online at a particular time, they can be used to detect and eliminate particular types of attacks which require withholding publications of the data to the network until a later time and then revealing the data suddenly (such as Bitcoin 51% attacks) and can be used to establish a total ordering on blocks. 

For example, Distributed blockchain consensus with a reliable timestamping server is trivial. The rule "Accept the block with the highest fees which was produced within 15 seconds of the previous block" achieves blockchain consensus. This rule uniquely determines a unique successor block. In fact if an accurate and honest timestamping service exists then this simple rule produces a 51% attack network with no mining and extremely low operational overhead.

The original Obelisk design was based upon constructing a distributed timestamping, but only worked in a fully connected graph.  No distributed time stamping system could achieve provable consensus on the total ordering of events between all nodes in the network using only the local information available to individual nodes. Each node only sees a subset of the network. The fully connected case of a small number of servers is a special case where each node has a "global" view and eventually arrives at the same data and consesus as all other nodes. Public broadcast channels and fully connected graphs make the byzantine generals problem fairly trivial.

While time stamp consensus and a full total ordering of events could not be achieved from the local information available to a node, randomized consensus allows provable global consenus from local information for non-pathological graph topologies. However, we were able to prove a weaker result which allows nodes to derive upper and lower bounds (a temporal interval) on events in the network. These bounds are local to each node or subset of nodes in the network and are very useful for detecting and preventing some type of Sybil attacks.


Distributed Time Stamping:
====

We show how you can create a distributed timestamping authority using the Obelisk public broadcast channel, time stamped blocks and receipts for block acknowledgements.

We want to create a system that allows us to prove with high certainty
- the publication time of a block 
- to establish that a node was active on the network and communicating 
- to prove that data existed and was published within a particular time interval
- prove that data did not exist at a time, or if it did exist was not published publicly

Having this information allows us to build detection systems for cheating nodes. We want to show with high probability that a particular node is selectively denying messages, creating invalid time stamps, belongs to a colluding subgraph of the network or is otherwise unreliable and untrustworthy.

Each node is subscribed to the block chain of a list of other nodes. Every few seconds each node publishes a new block. Each block is time stamped and includes a list of hashes (receipts) of the blocks the node has received since the last block it published. Each published block is cryptographicly signed by the publishing node's private key.

Each node is constantly publishing timestamped blocks and publishing receipts for blocks published by other nodes. This forms a dense, interlinking mesh of timestamps and receipts and counter receipts and make it very difficult for malicious node backdate events without detection.

The public broadcast channel imposes several constraints
- Once a block is published, it cannot be unpublished (blocks are replicated peer to peer to all subscribers. Once a block has been published, it spreads to all subscribers. You have to destroy all peers who have received the block to erase it from internet).
- A node cannot publish a different version of an earlier block without detection (blocks are numbered and it would be detected if the node signed two different blocks with the same sequence number)
- A node cannot backdate the time stamp on the receipt of a block, without delaying the publication of a block (timestamps only go up, time stamps increase monotonously with block sequence count)
- A block in the middle of the chain cannot be changed without invalidating every block that comes after it (linked time stamping, each block header contains a hash of the previous block)

Situation:

A publishes a block. B publishes a block with a receipt for the block published by A. Then A publishes a new block with a receipt of the Block by B.

Node A is subscribed to Node B. Node B is subscribed to Node A.

Example:
Node A publishes block A1 with time T1
Node B receives block A1
Node B publishes block B2 with time T2. B1 includes hash of block A1.
Node A receives block B2.
Node A publishes block A3 with time T3. A3 includes hash of block B2.


This is called a "2-cycle". If A trusts themselves and believes that their clock is honest, then A knows that block B2 existed and was published between times T1 and T3.

If B2 was published before T1, then B2 could not include the hash of A1, because A1 did not exist yet. The probaility of guessing the hash by luck is 1 in 2^256.

If B2 was published after T3, then A3 could not include the hash of B2, because A3 could not include a hash for a block that did not exist at the time A3 was created.

Therefore B2 must have been produced after A1 was published and before A3 was published. Therefore if the clock of Node A is accurate and honest, B2 was created and published between times T1 and T3.

Therefore this construction allows us to prove with certainty that events happened on certain temporal intervals with respect to Node A's clock. There are higher order cycles, 3-cycles, 4-cycles and so on in the receipt graph. This establishes a distributed time stamping system with a calculus of temporal intervals.

You can show that, if a block  X1  published at time T, a cycle starting at a honest node and ending on the same honest node ending on T2, that T < T2. This upper bounds the publication time. If we have a receipt for a trusted node of successor block X0 with timestamp T1, T1 < T. The timestamp of the receipt of the previous block (X0) lower bounds the time interval for the publication of X1. This is another way of producing intervals using the monotonously increasing clock assumption.

Some nodes are honest and do not lie. Some nodes try to lie about timestamps and the order messages were received. If we have a cycle between dishonest nodes, the time stamps can be anything, subject to the constraint of the public broadcast channel. However if the cycle of receipts contains at least one honest node then it places a constraint on the timestamps.

If we have a cycle of receipts, A -> B, B-> C, we say that the two cycles "interlink". Cycles between receipts within the subgraph of honest nodes interlink broadly. The multiple, interlinking timestamp and receipts form a dense interlinked mesh. If you say something existed at time 3, but did not publish it to network until time 8, all the honest nodes in network will have a timestamp of your block announcing the thing, with time greater than or equal to 8. Only nodes on a subgraph of lying or cheating nodes will have a lower timestamp.

Receipt Cycles Establish a Fair Total Ordering of Events with Respect to the Clock of a Given Node:

To prove that a block Z existed by time 5, we can find a sequence of blocks that reference each other by hash, X1 -> Y1 -> Z1 -> X2. If block X2 was published by a trusted/honest node with an accurate clock, the timestamp on block X2 upper bounds the time Z1 was published to the network, even if we do not trust the node that published block Y or the node that published Z. 

Choose a node X. We want to establish a temporal ordering on blocks with respect to X. We enumerate all cycles that originate at X (assume only cycles with one loop, cycles that start at X and end at X and do not pass through X multiple times). Each block will be contained in one or more cycles starting at X and ending at X. We say the time of a block with respect to X for a particular cycle is the time of the receipt produced by X that ends the cycle. For each event we choose the cycle with lowest ending timestamp, for each cycle that contains the event.

So if we have cycles
X1 (t=1) -> Y1 -> X2 (t=3)  (cycle starting at block X1, ending at block X2, timestamp on x1) is 1, x2 timestamp is 3)
X1 (t=1) -> Y1 -> Z1 -> X3 (t=5)

Here, 
- Y is subscribed to X
- X is subscribed to Y
- Z is subscribed to Y
- X is subscribed to Z

We have cycles X->Y->X and X->Y->Z->X.

X produces block X1, which has timestamp t=1. Block Yhas hash for block X1 in it, proving Y received the block. 

X publishes X2 with block showing receipt for Y1 (which contains receipt for X1)
Z publishes Z1 with receipt for Y1
X publishes X3 (with timestamp t=5) with receipt for Z1

Block Y1 is involved in two cycles of X in this example. If we trust the clock of X, then we know that Y1 existed and was published before t=3 (we take the lower of the two cycles). If Y1 was the successor to block Y0, then we can lower bound the time Y1 was published at the time stamp of the block by X which acknowledges Y0.

This produces a time upper and lower bound for any block that can be reached by a receipt chain from X and which leads back to X. For a well conditioned graph, this will include nearly all blocks. For upper bounds for block publication time we take the least of any cycle ending time. For lower bounds we take the greater of the cycle ending times for the predeceding block.

We can generalize this notion from "time with respect to node X" to time with respect to a subgraph of trusted nodes in the network. We take a subset of the network. We assume the nodes in the network have synced clocks and report time accurately. We allow a "cycle" that ends on any node in the subgraph and ends on any other node in the subgraph.

If nodes publish blocks every fifteen seconds or every minute, we can confidently bound the time interval of an event to a reasonably small time interval. We can show that things either did not exist at a given time or were not published to a causally accessible part of the network.

In a random graph of N nodes, where the block time per node is a constant k (say 15 seconds), the interval to which a random events can reliability be causally resolved assuming only a single trusted node, grows with an upper bound of  k*log(N). 


Methods to Eliminate the 51% Attack:
======

The distributed timestamping system can be used to prevent a 51% attack by even a majority of nodes, simply by rejecting and severing relationships with nodes who disconnect from the network and then reappear with provably backdated consensus decisions for blocks that were provably not published to the network at the claimed time.

Similarly, nodes can become automaticly untrusted for remaining connected to the network and spontaneously deciding to attempt to revert previously established consensus for no justifiable reason.

In Bitcoin the classical 51% attack, a miner with majority hash power forks the blockchain, keeping his blocks secret. The miner gets ahead of the network in secret and suddenly publishes his longer chain. The network instantly switches to the attackers longer chain. Transactions are reverted and coins may have been stolen from exchanges.

The evil miner deposited Bitcoin in an exchange, bought Litecoin, withdraws the litecoin and uses a 51% attack to revert the deposit transaction and get his Bitcoin back but keeping the Litecoin. Then he uses the Litecoin to buy back cheap Bitcoin after the theft hits the media. The miner further more buys put options on Bitcoin and further magnifies his gains. The evil miner also decides to rob a bank at the same time, by depositing Bitcoin, withdrawling the Bitcoin and then reverting the deposit transaction. He now has both the withdrawn coins and the coins he never deposited from any bank which has not taken extremely difficult security measures.

In Skycoin, the distributed time stamping system allows individual nodes to determine locally that a node witheld information from the network and suddenly published it in a 51% attack attempt. Each node locally evaluates the information and chooses whether to ignore the influence of the potentially malicious node. In this way, a successful attack in a random graph now requires over 80% to 90% of the influential network nodes, not merely a majority. The honest nodes simply detect and ignore the 51% attack attempt.

If each Node is informed by an indepedent but unreliable oracle for determining global consensus (each node samples consensus of a independent random subgraphs of the network), we believe the probability of a successful attack after a few block confirmations can be made arbritarily close to zero. This approach combines local information with indepedent random sampling of the global network state. Local state is used to determine and negotiate consensus and subgraphs of the global network are sampled to probabilistically determine if global network consensus has been reached and to detect netsplits.

Knowledge about the probability of global consensus on a block can be used to decide whether an attempt to fork an earlier block should be accepted. In the naive approach, if a majority of the nodes subscribed vote for a fork of an earlier block, the node will accept this fork.

With a global consensus oracle, the votes for the fork become weighted by the belief that the purposed changes are a result of the legitimite process through which nodes in the network come into agreement (the network is still arriving at global consensus), or whether agreement has already been reached unanimously a long time ago and this is merely an attack in an attempt to revert previous consensus (for which there is no valid valid after global consensus has become unamimous among the active nodes).

Another prospective approach uses a hybrid system of Ben Or randomized consensus on a web of trust to vote a commitee of trusted masternodes, who form a fully connected public Quorum which determines block consensus. The commitee election might be daily and more resources can be put into verifying global consensus on the single commitee election than verifying consensus on individual blocks.

We are looking at several different approaches. Skycoin consensus will change as we develop better algorithms and software infrastructure.