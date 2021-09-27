# yeet (Yeeting Everything Everywhere i Think)

basically i've fallen down a rabbit hole, so i'm writing a message broker. this message broker is intended to be core of the jaspr project.

the key concept here is simple, I want to make it easy to manage and deploy little networks, but still have them to form one big gigachad of a network

some terminology to make this process not suck

network - single yeet server and its clients 

cluster - network of yeet servers becomeing a mesh

the idea is the network works like you're simple pub sub model while the clusters function like the internet handling connections auto connects and distributing information about what networks are alreay present automatically. 

## stupid thoughts i had while writing this
this shit a baby internet in the internet.

ants


## YEET NETWORK PROTOCOL (shamelessly inspired from nats)
|PUB|SUB|UNSUB|INFO|CONNECT|ACK|MSG|PING|PONG|CLOSE|

## Clustering 

### How does a network join a cluster
1. a network asks another network to form a cluster with it
2. networks exchange their respective topic tables
3. start BFSing to share updated topic tables

### Cluster Optimization

#### Constraints
- networks in a cluster can be connected to a maximum of n other networks
  - except when adding a network to the cluster or changing over network connections (aka connect to new network then disconnect so you can always return to the old connection) 
- networks should never become fully disconnected from the cluster
- optimize for average time msgs take traveling through the network


### Ant Colony Optimization Approach


#### the forward way
1. send a message to a random network and give it a random target
2. keep sending it to networks till it finds its target
3. trace back to the source network , recording the time taken for each step along the way 
4. use that ping time to influence which networks messages are being sent to
5. repeat for each network trying to minimize the time that average time of all the packets traveling through this network is minimized 

#### the ass backwards way
1. look at the travel time sources and messages coming to the network node
2. use this to influence where packets are going 
3. repeat for each network trying to minimize the time that average time of all the packets traveling through this network is minimized
 

#### optimizations of the optimizer 
1. prefer targets based on the most common messages through that network

#### problems 
1. may be difficult to find better paths unless the parameters are tuned 
2. forward way requires custom
message type and back tracking 
