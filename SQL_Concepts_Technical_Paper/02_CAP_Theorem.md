# CAP Theorem in Distributed Databases

## 1. Introduction

CAP Theorem explains an important trade-off in distributed databases. A distributed database stores data across multiple servers or locations.

CAP stands for:

- Consistency
- Availability
- Partition Tolerance

The theorem says that when a network partition happens, a distributed system must choose between strong consistency and availability for that situation.

## 2. Consistency

Consistency means that every read gets the latest successful write, or an error. All users should see the same current value.

Example: If a product's stock is updated from 5 to 4, a read from another server should not show the old value 5 when strong consistency is required.

## 3. Availability

Availability means that every request to a working node receives a response, even if that response may contain older data.

Example: An online shopping application should continue responding to users even when one server cannot communicate with another server.

## 4. Partition Tolerance

A network partition happens when some servers cannot communicate with other servers because of a network failure.

Partition tolerance means the system continues operating despite this communication problem. In a distributed system, network failures can happen, so partition tolerance is usually necessary.

## 5. The CAP Trade-off

During a network partition, a system generally has two choices:

### CP: Consistency and Partition Tolerance

The system keeps data consistent, but some requests may be rejected or delayed until communication is restored.

Example: A system that must avoid giving the same item to two customers may temporarily stop some operations.

### AP: Availability and Partition Tolerance

The system continues responding, but different nodes may temporarily return different values. The data can become consistent later after servers communicate again. This is often called eventual consistency.

Example: A social media application may show a recently changed profile picture on one server before another server receives the update.

### What about CA?

Consistency and availability can be provided when there is no network partition. But during a partition, a distributed system cannot guarantee both strong consistency and availability for every request.

## 6. Comparison

| Choice | Main behaviour during a partition |
|---|---|
| CP | Keeps consistency; may reject or delay requests |
| AP | Keeps responding; may return temporarily different data |
| CA | Not a complete choice during a network partition |

## 7. Conclusion

CAP Theorem helps developers understand the trade-offs in distributed database design. The correct choice depends on the application. Systems that handle payments may prefer consistency, while some social or content applications may prefer availability.
