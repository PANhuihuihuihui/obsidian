#### What is Distributed System
eg: Google's objectives in serving query?
- fast/alway online/ scaleablity / correctness/ 
- resilience to failures Low latency Most relevant results
#### What make a system Distributed
- Build reliable systems with unreliable components
- Aggregate systems for higher capacity
- Conquer geographic separation
- Customize computers for specific tasks
eg: back-end about bank: how to auto-update all copies
1. Concurrency: Synchronize by exchanging messages
	Network delay, unreliable. comupter unrealiable
2. partial failures
3. ambiguous failures
4. performance at scale, testing

#### Objective 
Unify several machines from app perspective
Enable concurrent use, hide failures
Do “heavy lifting” so developers don’t need to

### Distrubition data processing
eg Failure log analysis
1. Distributed data storage
	Partition input data across many disks
	Compute on a single server can be **bottleneck**
2. Distrubuted Data Processing
	Partition input, process partitions in parallel, merge outputs
	**final computation capcity**, **one machine break down**

Desirable Properties
- Scalable: Performance grows with # of machines
- Fault-tolerant: Can complete execution despite machine failures
- Simple: Minimize expertise required of programmer
- Widely applicable: Should not restrict kinds of processing feasible

The Need for scaleable data processing: 23andMe(genen match) Google(Page Rank)

### MapReduce
![](https://raw.githubusercontent.com/PANhuihuihuihui/PicBed/main/202209140307515.png)
Hello word example: Word Count
```go
map(key, value): //filename, file contents
for each word w in value:
	EmitIntermediate(w, "1");
	
reduce(key, list(values)): //word, counts
int result = 0;  
for each v in values:
	result += ParseInt(v);
Emit(AsString(result));
```
Google: PageRank
compute rank for web page P as average rank of pages that link to P
Initialize rank for every page to a random value
Map(a web page W, W's contents)
	for every web page P, that W link to, output (P,W)
Reduce(web Page P, {set of pages that link to P})
	output rank for P as average rank of pages that link to P
```go
map(key,value) // topageUrl, self rank
EmitIntermediate("google.com",100)

reduce(key,list(values)):
int resutl = 0;
for each v in values:
	result += ParseInt(v);
result/= len(values)
Emit(AsString(result));
```
> When can a Reduce task begin excuting? 

Master does not touch any data
![](https://raw.githubusercontent.com/PANhuihuihuihui/PicBed/main/202209162126809.png)


### Handling Master Failure
must relicate Master state to torlerate faulure
eg: Replicating Bank Database: Inconsistent replicas (interest >> deposit )
solution: timestap?  must in same order!
Synchronizing Replicas: Replicated state machine
### Implementing RSM: Task 1
Order updatae by time of recipt relica ID: **clock not in sync** 
Solution: 
1. leverage GPS broadcaset ( not work indoors )
2.  skew based on reference clock:Clock driff Unbounded network delay(rely on timeserver availablity)
![](https://raw.githubusercontent.com/PANhuihuihuihui/PicBed/main/202209211853384.png)
3. NTP(Network time potorcal)
#### Logical clocks
**Time nature:** Only relationships between events matter(1978 paper by Leslie Lamport)
**Define" happpends before"**
1. same process if a occurs before b, then a -> b
2. If c is a message receipt of b,then b -> c
3. If a -> b ab -> c,then a -> c
**Lamport Clock algorithm**
1. before executing an event Ci <- Ci +1
2. set Cj and time of recevie event to 1 + max{Cj, C(m)}

Hence, we only need to let the relicas have the same state "order of event are same", what if logical order is not like that?
real world a < b ?  the processing between the relicas must be done between notifiy user
processing id?  IP is solution, only let them unique


#### RSM with Lamport Clocks
![](https://raw.githubusercontent.com/PANhuihuihuihui/PicBed/main/202209230508738.png)
relicas logic: 
1. clock label: 1+ max(current, receive)
2. excuate: 
	current < receive -> do self op 
	current > receive -> do the receive op, self op wait
	**Important fact:** all the message receive in order! TCP conncetion make it possible "we don't have to warry about that there are some op with lower order on its way"

#### Reduce waiting
- periodcally ping all the nodes to sync the clock
- torlerate temporaray insconsitency 
	- Apply updata imediately upon receipt
	- maintain log of updates in order to rollback

#### Causal ordering
Ordering all updates may be unnecessary
a -> b implies C(a) <C (b)
but reverse is not ture! 

#### Vector clock(system log)
No. of components = No. of processes
ci is a count of events in process i that causally precede e
![](https://raw.githubusercontent.com/PANhuihuihuihui/PicBed/main/202209230637577.png)
- a happend before event b: for every k a_k ≥ b_k V(a) ≠ V(b)
- a || b : for some k a_i ≥ b_i , a_j ≤ b_j
V(a) < V(z) if and only if there is a chain of events linked byàbetween a and z

is this enough？ 
If one relica down, all the replicas cannot progress
**Nee to be able to replace replicas**

#### Primary Backup Replication
How to handle primary failure?
- promote one of the backups as the primary
How to handle backup failure?
- pick some free machine 

#### exmaple MapReduce Master
when to sync again
```
receive msg and parse addr
pick task to assign
mark task as assigned
respond with task assignment
<< this is the best place
```
- bank example: not works
Takeaways:  okay for primary to be out of sync with back untill change is externally visible
Hece, better  receive the backup success before send response to user.

#### what to transfer in sync
- snapshot of primary's state
	slow(everything), but useful when bootstrapping new backup
- Every operation(small message)
	leverage the determinism of state machine


#### Client perspective
- what client need to know： which machine is priamary
- hard code to client?: No could be failled
- How does client discover current primary: **View Service**
 view service down? possible "assume not down at this stage"
#### View service
- Maintain current membership of primary-backup sevice.(View number, proimary backup)
- When to change:  primary fails or backup fails
- How to know it is fail: Periodically exchange heartbeat message
- How to konw if the backup is up-to-date
	Primary applies op but fails before syncing with backup： client will resend so it is fine, resend to 2
	Primary fails before new backup is initialized: GG
	(1, S1, \_) -> (2, S1, S2) -> (3, S2,\_)
	**View change has three steps:**
	-  View service announces new view
	- Primary syncs with new backup if there is one
	- Primary acknowledges new view: 
	- View service knows backup is up-to-date once it receives **ACK** for new view from primary
	- **Stuck** if primary fails in midst of view change (before ACK)
	-  What if S1 fails before it bootstraps S2? ok
	View 发现 S2， 1. 我决定了 新的view 是（2，S1， S2）， client来问我我就说这个。 2. S1 你处理一下S2. 3. 收到ACK 找找有没有S3，或者S1 dead 我就变成（3，S2， \_）. 没收到 ACK 只能等着。
	What if we hav two backup, which one to be decide to be primary： Does not matter, as long as New backup have to sync with other backup to make sure every one is on same page.

#### Scalability of View service
Too much load on view service if all clients contact it before every operation
Clients can cache view across operations
When to invalidate cached view?
When no/**negative** response from primary (I am not primary)
#### Avoid split Brain
**Split Brain**
client and server all believe they are correct.  not the truth
- Primary must forward all opertation to backups
	Get  ACKs from backups that they both agree view is unchange
![](https://raw.githubusercontent.com/PANhuihuihuihui/PicBed/main/202209250400272.png) more prictcal! 
Why can’t it be the case that backups are also unaware of view change?
	If view did change, only a backup can be promoted as primary
![](https://raw.githubusercontent.com/PANhuihuihuihui/PicBed/main/202209250330883.png)

#### Ordering of Updates
All updates must be applied in the same order at all replicas
How is the order being determined?Primary effectively serializes all writes

#### Serving Reads
 we want the backups could be read from, but acturally not permit
 
 What if primary’s state is ahead of backup?
	 -  Updates to primary not yet externally visible
	 - Effect of read equivalent to if primary fails at this point
What if backup’s state is ahead of primary?
	Different backups may not be in sync
	Primary may get replaced before it applies update
![](https://raw.githubusercontent.com/PANhuihuihuihui/PicBed/main/202209250342175.png)


#### Desired properites
- All writes are totally ordered
- Once read returns particular value, all later reads should return that value or value of later write
- Once a write **completes**, all later reads should return value of that write or value of later write (complete is when backup return ACKs)
- just like one machine
#### Linearizability
total ordering of writes  
Read returns last completed write

#### Consistency Spectrum
 ![](https://raw.githubusercontent.com/PANhuihuihuihui/PicBed/main/202209250350229.png)
 Latency vs. consistency tradeoff
