Networking overlays:

-> network overlays in kubernetes cluster are used to address container,pod,service,and exernal clinet connectivity


kubernetes network model:


Every pod get its own ip address
you do not have to create links between pods


-> container-to-host port mapping is simplified
-> pods are treated like vms for port allocation,naming,service discovery,load balancing,application configuration, and migration.

-> pod can communicate with all pods on all nodes without NAT

->agents(daemons, kubelets) on a node can communicate with all pods on that node.

overlays and underlays:

overlays are software components that decouple the physical infracture from the networking services

overlays encapsulate a packets within a packet to achieve connectivity and routing

-> an voirelay is a virtual netowrk service on the underlying network or underlay

-> an undrelay is the physical infrastructure supporting the connectivity.



Flannel:

flannel is virtual network designed for kubernetes,
-> each host in a flannel cluster run an  agent called flannelId.
_> it assiigns each host a subnet with acts as ip address pool for containers running on the host


-> container can then contract other containers directly, using their IP address

-> Flannel supports multiple backends for encapsulationg packets
-> the recommended choice is virtual extensible LAN,
-> which runs a Layer 2 network on top of a Layer 3 innfrastructure.

-> Flannel also supports host-gw which maps direct routes between hosts in a manner similar to calico

-> Flannel is an opensource project managed by CoreOS


project Calico:

Calico allow strong network policy managment and access control list(ACLs) you can configure inbound and outbound rules by port, direction, protocol and other attrubutes

-> similar to Flannel, calico runs an agent on each host. calico use a layer 3 approach to networking.

-> Calico connects hosts using the border gateway protocol(BGP) Each host run on BGP client, which tracks routes and distrubutes them to other hosts.

-> this reduces overhead, and scales and distributes  clusters more easily

-> calico is an open-source project maintained by tigera, INC


weave Net: 

weave net is a networking solutions offering a virtual networking with service discovery, policy managment, and fault tolerance,
-> weave net automatically routes around network failures and can link container hosted in different data centers using multi-cloud networking

weaveDNS provides name resolution, automated service discovery, load balancing and fault tolerance in addition weavenet include a  built in encryption system for securing all traffic between hosts

weave net is an opensource project maintained by weaveworks

Canal:

canal combines two projects : flannel and calico

it creates a unified networking solution that combines flannel networking architecure with calico's policy managment API

canal is more of a deployment tool for installing and configuring both flannel and calico , as well as integrating them into your orchestration engine.

the result is an opensource networking fabric with built-in policy managment that leverages the best components of both networking tools

canal is an open-source project hosted by tigera



Network policies:

Pod Isolation 
By deafault, pods accept traffic from any source. the network policy resources in kubernetes provides a means of configuraing weather connections are accepted ro refused




