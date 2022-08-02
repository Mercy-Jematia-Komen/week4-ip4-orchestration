Design of StatefulSet
The StatefulSet will create N-replica Pods define under .spec.replicas. The Pod identity starts from 0 to N-1 ordinal set.
Network Identity
The Pods that are defined under a StatefulSet will have a hostname construct with $(statefulset name)-$(ordinal). So, hostnames will be [mongod-0, mongod-1, mongod-2].
The domain name is known as connection string for database connectivity will be identified as
 $(service name).$(namespace).svc.cluster.local
 The service will run as a Headless Service to manage the domain of a Pod. In general understanding of Headless Service, there is no need for LoadBalancer or a kube-proxy to interact directly with Pods but using a Service IP, so the Cluster IP is set to none.
 Deployment and Scaling of StatefulSet
Pods are deployed in {0..N-1} order for a StatefulSet of N-replicas.
The termination of Pods is performed in reverse {N-1..0}.
The execution of a Pod depends on other ordinal index Pods to be running and active.
The termination of a Pod also required other ordinal index Pods has to be terminated before.
