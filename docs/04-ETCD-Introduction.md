## ETCD for Beginners

### What is a ETCD?
 - Etcd is an open-source distributed key-value store that is used to store and manage the information that distributed systems need for their operations. It stores the configuration data, state data, and metadata in Kubernetes.

### What is a Key-Value Store?
- Traditionally, databases have been in tabular format, you must have heared about SQL or Relational databases. They store data in rows and columns.

![Relational databases](./images/relational-dbs.PNG)

- A Key-Value Store stores information in a Key and Value format.
  
![ETCD](./images/ETCD.png)

- When you start ETCD it will by default listens on port 2379

- The default client that comes with ETCD is the etcdctl client. You can use it to store and retrieve key-value pairs. 