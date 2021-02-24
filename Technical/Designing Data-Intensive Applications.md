## Designing Data-Intensive Applications
___
### Chapter 1 - Reliable, Scalable, and Maintainable Applications
- There are a lot of different databases that are suited for different kinds of applications. We have to figure out what the best ones are for the job.
- Lots of datastores now and it can be difficult to categorize them.
- Many applications use multiple data stores to meet processing and storage needs.
- When designing a data storage system, some questions:
	- How do you ensure the data is correct and complete?
	- How do you provide good performance to clients?
	- How do you scale?
- THREE MAIN CONCERNS when designing software:
	- **Reliability**: continuing to work correctly, even when things go wrong.
		- Faults: when a single component deviates from spec.
		- Failure: when the whole system stops providing the required service.
		- It's better to tolerate faults than prevent them.
		- Reliability is also concerned with reducing human errors by making the system simple to use, hiding the areas where people make the most mistakes, logging and monitoring, etc. CONFIGURATION ERRORS ARE LEADING CAUSE OF OUTAGES.
	- **Scalability**: a system's ability to cope with increased load.
		- "If the system grows in a particular way, what are our options for coping with the growth?"
		- Load: needs to be described by "load parameters," e.g. requests per second to a server, ratio of reads to writes, number of enrollees online, hit rate on cache... 
		- Twitter example: They zeroed in on two critical operations, posting a tweet and viewing the home timeline and then designed for scalability with those in mind. Their strategies changed as the platform gained steam by doing things like treating a celebrity's tweets differently from a normie's.
		- Once you have load factors, you can investigate what happens to the system when those load factors increase. Does CPU / memory go up? If so, how much do you have to increase specs in order to keep performance high?
			- "Performance" can mean different things. e.g., Hadoop cares about throughput and how long it takes to run a job. A web server will care more about how long it takes to deliver a response after receiving a request.
			- "Latency" is the time a request is waiting to be handled.
			- Response time should be thought of as a distribution of values, not a single. **Use percentiles**, like the median at p50. Also look at how bad outliers are in the p95-99 areas, aka "tail latencies". Percentiles are good to use for SLAs / SLOs (Service Level Objectives) anyhow.
		- How to cope with load?
			- Scale up (get better hardware)
			- Scale out (get more hardware and distribute load, aka "shared-nothing architecture").
			- Usually good plans end up doing a mix of both.
			- "Elastic": systems that can AUTOMATICALLY add resources as load increases.
			- "An architecture that scales well for a application is built around assumptions of which operations will be common and which will be rare - the load parameters."
	- Maintainability: designing software in such a way that it will minimize pain during maintenance. Pays attention to three principles:
		- Operability: making routine tasks easy, allowing the ops team to focus their efforts on high-value activities. e.g.: providing good monitoring and logging, support for automation and integration with standard tools, good documentation, self-healing...
		- Simplicity: Actively managing complexity and its symptoms. Reducing complexity improves the maintainability of software. FINDING GOOD ABSTRACTIONS (see "A Philosophy of Software Design")
		- Evolvability: Make changes easy. Goes back to simplicity and good abstractions, agile mindset.
___
### Chapter 2 - Data Models and Query Languages
- Relational databases: organizes data into "relations" (which are tables), where each relation is an unordered collection of "tuples" (rows).
- NoSQL: "Not Only SQL". Main drivers:
	- Wanting greater scalability for huge datasets or very fast writes / throughput
	- Wanting to use open source software
	- Using specialized queries not well-supported by relational
	- Frustration with strict schemas.
- "Polyglot persistence": Using relational along with nonrelational in the same app.
- "Impedance mismatch": The fact that a relational database


**Purpose For Reading**
- What am I hoping to get out of reading this?
 
**Main Takeaways & Metacognition**
- What are the major themes / points made?

**What can I do with this?**
- What actions am I going to take based on this book, if any?

**Personal Bottom Line**
- x/10
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTYyMzAxNjI0NCwxNjU2Njc0ODU1LC03Mj
E4OTcwNzcsLTE2MjM3MTIxMjQsNjQyMTM2MzUsLTI1MjA3MjI4
NCwtMjAzMTQ3NzY4Ml19
-->