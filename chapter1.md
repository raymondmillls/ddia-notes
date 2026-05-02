# Reliable, Scalable, and Maintainable Applications

Components of data intensive applications:
- **databases**: store data to be found later
- **caches**: remember the results of expensive operations to speed up reads later
- **search indexes**: allow users to search data by keyword or filter it
- **stream processing**: sends messages to other processes to be handled asynchronously
- **batch processing**: periodically crunches large amounts of accumulated data

## Thinking About Data Systems
Many tools for data storage and processing exist that are optimized for a variety of use cases

We need to think of the tradeoffs during tool selection, and how various tools can be used together to achieve *reliability*, *scalability*, and *maintainability*

## Reliability
**Reliability**: The system should continue to work *correctly* even in the face of *adversity*
- *faults* are the things that can go wrong with the system, and systems cope with them by being *fault tolerant* or *resilient*
- *failures* are when the system stops providing the required service to the user
- we want to design a system that is fault tolerant, as it is impossible to be fault-proof, one way of doing so is by deliberately inducing faults

### Hardware Faults
We can tolerate hardware faults using *redundancy* and tolerating loss of machines by prioritzing *elasticity* over single machine reliability

### Software Errors
To tolerate software faults, we can think of the gaurantees of the system and have the system constantly check itself while running and raise an alert if a discrepancy is found

### Human Errors
Human errors cause most outages, and we can address them by:
- Designing systems that minimize opportunities for failure
- Couple places where there are opportunities for mistakes from places they can cause failures
- Test thoroughly (unit tests and system integration tests)
- Allow quick and easy recovery from human errors
- Detailed and clear monitoring with performance metrics and error rates
- Good management practices and training

## Scalability
**Scalability**: As the system *grows*, there should we ways of dealing with growth

### Describing Load
We can describe load using *load parameters*
- We use load parameters that depend on the architecture of the system and which bottlenecks are most important

### Describing Performance
Once load has been described, you can investigate what happens when load increases. This can be viewed in two ways:
1. If you keep system resources the same when increasing a load parameter, how is performance affected?
2. If we increase a load parameter, how much do you need to increase the resources if you want to keep performance unchanged?

To answer these questions, we need **performance numbers**
- **throughput**: the number of records we can process per second
- **response time**: what a client sees
- **latency**: duration a request is waiting to be handled
- **median** is a good metric because it tells you 1/2 of requests are below and 1/2 are above the median, we can then convert these into *percentiles*

**Servive Level Objectives (SLOs)**: Define expected performance of a service
**Service Level Agreements (SLAs)**: Define availability of service

#### Approaches for Coping with Load
*Key question*: Now that we have *load parameters* and *performance numbers*, how do we maintain good performance when load increases?

**Veritical scaling**: Moving to a more powerful machine
**Horizontal scaling**: Distributing load across multiple smaller machines (aka *shared nothing* archiecture)
- *Elastic* systems automatically add compute resources when a load increase is detected, this is useful if load is highly unpredictable, but manually scaled systems are simpler and have less operational surprises
- There is no one size fits all architecture as it is highly specific to the application's SLOs, SLAs, and gaurantees

## Maintainability
**Maintainability**: Over time many people should be able to work on the system *productively*

Most of the cost of software systems is in maintenance and not development. Therefore, we must pay atention to *three design principles* for software systems:
1. **Operability**: Make it easy for operations teams to keep the system running smoothly
2. **Simplicity**: Remove complexity from the system so it can be understood easily
3. **Evolvability** (e.g., *extensibility*, *modifiability*, *plasticity*): Make changing the system easy, so it can be adapted for unanticipated use cases as requirements change

### Operability: Making Life Easy for Operations
Good operability means making routine tasks easy, allowing operations teams to focus their effort on high-value activities

### Simiplicity: Managing Complexity
Making a system simple does not necessarily mean reducing functionality, but removing *accidental complexity*
- **accidental complexity**: complexity that is not inherent in the problem the software solves, but that has arose from the implementation
- **abstractions**: a good abstraction can hide a complex implementation behind a simple to understand interface

### Evolvability: Making Change Easy
**agile**: working patterns that provide a framework for adapting to change
- The easy with which we can modify a data system and adapt it to changing requirements is closely linked to its simplicity / abstractions

