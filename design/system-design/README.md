# System design

## Step 1. Clarify Requirements and Specs

First things first, the ultimate goals should always be clear.&#x20;

Pinterest is a highly scalable photo-sharing service:&#x20;

* features: user profile, upload photos, news feed, etc.&#x20;
* scaling out: horizontal scalability and micro services.

## Step 2. Sketch Out High Level Design

Do not dive into details before outlining the big picture. Otherwise, going off too far towards a wrong direction would make it harder to even provide a roughly correct solution. We will regret wasting time on irrelevant details when we do not have time to finish the task.&#x20;

OK, let us sketch out the following diagram without concerning too much about the implementation detail of these components.

## Step 3. Discuss individual components and how they interact in detail

When we truly understand a system, we should be able to identify what each component is and explain how they interact with one another. Take these components in the above diagram and specify each one by one. This could lead to more general discussions, such as the three common topics in Section 2, and to more specific domains, like how to design the photo storage data layout…

### 3.1 Load Balancer

Generally speaking, load balancers fall into three categories:

* DNS Round Robin (rarely used): clients get a randomly-ordered list of IP addresses.
  * pros: easy to implement and free
  * cons: hard to control and not responsive, since DNS cache needs time to expire&#x20;
* L3/L4 Load Balancer: traffic is routed by IP address and port. L3 is network layer (IP). L4 is session layer (TCP).
  * pros: better granularity, simple, responsive
* L7 Load Balancer: traffic is routed by what is inside the HTTP protocol. L7 is application layer (HTTP). It is good enough to talk in this level of detail on this topic, but in case the interviewer wants more, we can suggest exact algorithms like round robin, weighted round robin, least loaded, least loaded with slow start, utilization limit, latency, cascade, etc.

### 3.2 Reverse Proxy

Reverse proxy, like varnish, centralizes internal services and provides unified interfaces to the public. For example, www.example.com/index and www.example.com/sports appear to come from the same domain, but in fact they are from different micro services behind the reverse proxy. Reverse proxy could also help with caching and load balancing.

### 3.3 (Frontend) Web Tier

This is where web pages are served, and usually combined with the service / backend tier in the very early stage of a web service.&#x20;

#### Stateless&#x20;

**There are two major bottlenecks of the whole system – requests per second (rps) and bandwidth.** We could improve the situation by using more efficient tech stack, like frameworks with async and non-blocking reactor pattern, and enhancing the hardware, like **scaling up (aka vertical scaling) or scaling out (aka horizontal scaling)**.&#x20;

Internet companies prefer scaling out, since it is more cost-efficient with a huge number of commodity machines. This is also good for recruiting, because the target skillsets are equipped by. After all, people rarely play with super computers or mainframes at home.&#x20;

**Frontend web tier and service tier must be stateless in order to add or remove hosts conveniently, thus achieving horizontal scalability.** As for feature switch or configs, there could be a database table / standalone service to keep those states.&#x20;

#### Web Application and API&#x20;

**MVC(MVT) or MVVC** pattern is the dominant pattern for this layer. Traditionally, view or template is rendered to HTML by the server at runtime. In the age of mobile computing, view can be as simple as serving the minimal package of data transporting to the mobile devices, which is called web API. People believe that the API can be shared by clients and browsers. And that is why single page web applications are becoming more and more popular, especially with the assistance of frontend frameworks like react.js, angular.js, backbone.js, etc.

### 3.4 App Service Tier

**The single responsibility principle** advocates small and autonomous services that work together, so that each service can do one thing well and not block others. Small teams with small services can plan much more aggressively for the sake of hyper-growth.&#x20;

#### Service Discovery

How do those services find each other? Zookeeper is a popular and centralized choice. Instances with name, address, port, etc. are registered into the path in ZooKeeper for each service. If one service does not know where to find another service, it can query Zookeeper for the location and memorize it until that location is unavailable.&#x20;

Zookeeper is a CP system in terms of CAP theorem (See Section 2.3 for more discussion), which means it stays consistent in the case of failures, but the leader of the centralized consensus will be unavailable for registering new services.&#x20;

In contrast to Zookeeper, Uber is doing interesting work in a decentralized way, named hyperbahn, based on Ringpop consisten hash ring. Read Amazon’s Dynamo to understand AP and eventual consistency.&#x20;

#### Micro Services&#x20;

For the Pinterest case, these micro services could be user profile, follower, feed, search, spam, etc. Any of those topics could lead to an in-depth discussion. Useful links are listed in Section 3: Future Studies, to help us deal with them.&#x20;

However, for a general interview question like “design Pinterest”, it is good enough to leave those services as black boxes.. If we want to show more passion, elaborate with some sample endpoints / APIs for those services would be great.

### 3.5 Data Tier

Although a relational database can do almost all the storage work, please remember **do not save a blob, like a photo, into a relational database, and choose the right database for the right service**. For example, read performance is important for follower service, therefore it makes sense to use a key-value cache. Feeds are generated as time passes by, so HBase / Cassandra’s timestamp index is a great fit for this use case. Users have relationships with other users or objects, so a relational database is our choice by default in an user profile service. Data and storage is a rather wide topic, and we will discuss it later in Section 2.2 Storage.

## Step 4. Back-of-the-envelope Calculation

The final step, estimating how many machines are required, is optional, because time is probably up after all the discussions above and three common topics below. In case we run into this topic, we’d better prepare for it as well. It is a little tricky… we need come up with some variables and a function first, and then make some guesses for the values of those variables, and finally calculate the result. The cost is a function of CPU, RAM, storage, bandwidth, number and size of the images uploaded each day.

* N users 1010
* i images / (user \* day) 10
* s size in bytes / image 106
* viewed v times / image 100
* d days • h requests / sec 104 (bottleneck)
* b bandwidth (bottleneck)
* Server cost: $1000 / server
* Storage cost: $0.1 / GB
* Storage = Nisd&#x20;

Remember the two bottlenecks we mentioned in section 1.3.3 Web Tier? – requests per second (rps) and bandwidth. So the final expression would be&#x20;

Number of required servers = max(Niv/h, Nivs/b)
