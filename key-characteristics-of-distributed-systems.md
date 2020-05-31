# Key Characteristics of Distributed Systems

## Reliability

* Work as expected
* Fault-tolerant

Faults - a component of the system deviates from its spec.

Failure - the entire system stops working.

It's impossible to eliminate every possible kind of fault. We should design a fault-tolerance mechanisms that prevent faults from causing failures.

Fault can be:

* Hardware faults. E.g. hard disks crash.
* Software faults. E.g. unexpected input breaks the software, DB crash.
* Human errors. E.g. configuration error caused by operator.

How to increase reliability:

* Design systems in a way that minimizes opportunities for error. For example,

  well-designed abstractions, APIs, and admin interfaces make it easy to do “the

  right thing” and discourage “the wrong thing.”

* Decouple the places where people make the most mistakes from the places where

  they can cause failures. For example, sandbox environment v.s. production environment.

* **Test** thoroughly at all levels, from unit tests to whole-system integration tests and

  manual tests

* Allow quick and easy **recovery** from human errors, to minimize the impact in the case of a failure.
* Set up detailed and clear **monitoring**, such as performance metrics and error

  rates.

## Scalability

The ability to cope with increased load.

Define **Load**. Example: how many requests you get per second.

Define **Performance**. Example: the throughput of the system.

Usually it's better to use **percentiles** than **mean**. Example, high percentiles of response time \(aka. **tail latencies**\). For example, Amazon describes response time requirements for internal services in terms of the 99.9th percentile, even though it only affects 1 in 1,000 requests. This is because the customers with the slowest requests are often those who have the most data on their accounts because they have made many purchases—that is, they’re the most valuable customers.

**Service level objectives** \(SLO\) and **service level agreements** \(SLA\) are often default using percentiles.

* Availability
* Efficiency
* Manageability

