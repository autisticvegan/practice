https://martinfowler.com/articles/patterns-of-distributed-systems/paxos.html


Problem

When multiple nodes share state, they often need to agree between themselves on a particular value. With Leader and Followers, the leader decides and passes its value to the followers. But if there is no leader, then the nodes need to determine a value themselves. (Even with a leader-follower, they may need to do this to elect a leader.)

A leader can ensure replicas safely acquire an update by using Two Phase Commit, but without a leader we can have competing nodes attempt to gather a Quorum. This process is further complicated because any node may fail or disconnect. A node may achieve quorum on a value, but disconnect before it is able to communicate this value to the entire cluster.

Solution

The Paxos algorithm was developed by Leslie Lamport, published in his 1998 paper The Part-Time Parliament. Paxos works in three phases to make sure multiple nodes agree on the same value in spite of partial network or node failures. The first two phases act to build consensus around a value, the last phase then communicates that consensus to the remaining replicas.

    Prepare phase: establish the latest Generation Clock and gather any already accepted values.
    Accept phase: propose a value for this generation for replicas to accept.
    Commit Phase: let all the replicas know that a value has been chosen.

In the first phase (called prepare phase), the node proposing a value (called a proposer) contacts all the nodes in the cluster (called acceptors) and asks them if they will promise to consider its value. Once a quorum of acceptors return such a promise, the proposer moves onto the second phase. In the second phase (called the accept phase) the proposer sends out a proposed value, if a quorum [1] of nodes accepts this value then the value is chosen. In the final phase (called the commit phase), the proposer can then commit the chosen value to all the nodes in the cluster.