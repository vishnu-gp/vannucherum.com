---
layout: post
title:  "Scalability 101: Horizontal vs Vertical, and Where the Bottlenecks Hide"
author: gp
categories: [System Design, HLD]
image: https://res.cloudinary.com/vannucherum/image/upload/v1763144084/vannucherum.com/posts/2025-11-15-scalability-101-horizontal-vs-vertical-and-where-the-bottlenecks-hide/cover_kl3j9q.jpg
tags: [scalability, architecture, distributed-systems, performance]
description: "A practical guide to horizontal and vertical scaling trade-offs and the bottlenecks that limit both throughput and latency."
featured: true
hidden: false
rating: 5
---

We’ve all done it at some point:

> “Traffic is spiking, users are complaining. Quick — double the number of instances.”

The graphs look nicer, CPU goes down, everyone relaxes… and yet some users *still* stare at spinners, and your key flows are still sluggish under load.

This post is about **why that happens**.

Not just “horizontal vs vertical scaling” in theory, but how it ties to:

- **Throughput vs latency**
- **Amdahl vs Gustafson mental models**
- **Stateful vs stateless design**

…and why blindly adding more instances often doesn’t help as much as you expect.

---

## Scalability in two axes: throughput vs latency

Before we even say “horizontal” or “vertical”, it helps to split scalability into two simple questions:

1. **Throughput** – *How many* requests per second can the system handle?
2. **Latency** – *How long* does a single request take end-to-end?

You can think of it like a restaurant:

- **Throughput**: How many customers you can serve per hour.
- **Latency**: How long one customer waits from ordering to eating.

In systems:

- Throughput → requests/second, jobs/minute, events processed per hour.
- Latency → p95 response time, time until a job is done.

Scaling decisions affect these **differently**:

<!-- | Dimension  | Vertical Scale                                  | Horizontal Scale                                                 |
|-----------|--------------------------------------------------------------|-------------------------------------------------------------------------------|
| Throughput| Improves, but with diminishing returns as resources saturate | Often improves close to linearly *until* you hit shared bottlenecks          |
| Latency   | Often improves (faster CPU, more RAM → less contention)      | Often unchanged; shared state and remote calls usually dominate per-request  | -->

<table style="border-collapse: collapse; width: 100%;">
  <thead>
    <tr>
      <th style="border: 1px solid #ddd; padding: 8px;">Dimension</th>
      <th style="border: 1px solid #ddd; padding: 8px;">Vertical scale</th>
      <th style="border: 1px solid #ddd; padding: 8px;">Horizontal scale</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="border: 1px solid #ddd; padding: 8px;"><strong>Throughput</strong></td>
      <td style="border: 1px solid #ddd; padding: 8px;">Improves, but with diminishing returns as resources saturate</td>
      <td style="border: 1px solid #ddd; padding: 8px;">Often improves close to linearly <em>until</em> you hit shared bottlenecks</td>
    </tr>
    <tr>
      <td style="border: 1px solid #ddd; padding: 8px;"><strong>Latency</strong></td>
      <td style="border: 1px solid #ddd; padding: 8px;">Often improves (faster CPU, more RAM → less contention)</td>
      <td style="border: 1px solid #ddd; padding: 8px;">Often unchanged; shared state and remote calls usually dominate per-request</td>
    </tr>
  </tbody>
</table>



If you only watch throughput graphs (“No 500s, traffic handled, we’re good”), it’s easy to miss that your **latency** is slowly creeping up because a shared component is screaming for help.

---

## Vertical vs horizontal scaling

Let’s name them quickly and honestly.

### Vertical scaling – “make the box bigger”

You scale **up**:

- Move from 4 vCPUs → 16 vCPUs
- Add RAM, faster disks, better network

**Pros**

- Simple architecture (monoliths love this).
- No sharding complexity, no cross-node coordination.
- Great for early-stage systems: you focus on building features.

**Cons**

- Hard limits: you’ll eventually hit the largest available machine (or cost ceiling).
- Single point of failure / blast radius.
- Non-linear cost: high-end instances are disproportionately expensive.

### Horizontal scaling – “add more boxes”

You scale **out**:

- Add more app instances behind a load balancer.
- Shard a database.
- Add more workers to a queue.

**Pros**

- Better fault isolation (one node dying isn’t the end of the world).
- Potentially near-linear throughput scaling for well-partitioned workloads.
- Fits cloud-native elasticity stories (autoscaling).

**Cons**

- Distributed systems complexity (consistency, coordination, retries).
- Latency can get worse if you add cross-node chatter.
- You still have to deal with **shared state**.

And that’s the punchline: **shared state is where your bottlenecks hide.**

---

**Before** – classic “we scaled the app but not the DB”:

<img src="https://res.cloudinary.com/vannucherum/image/upload/v1763143882/vannucherum.com/posts/2025-11-15-scalability-101-horizontal-vs-vertical-and-where-the-bottlenecks-hide/1_c4dkrz.svg"/>

**After** – same app tier, but state is scaled or offloaded:

<img src="https://res.cloudinary.com/vannucherum/image/upload/v1763143878/vannucherum.com/posts/2025-11-15-scalability-101-horizontal-vs-vertical-and-where-the-bottlenecks-hide/2_u1x6zh.svg"/>


You’ve not “fixed” everything, but you’ve moved the bottleneck instead of pretending it doesn’t exist.

---

## Where horizontal scaling doesn’t help (much)

Let’s walk through a realistic scenario.

You have 4 API servers and 1 database. Under a traffic spike, APIs hit 80% CPU, DB hits 90% CPU and IOPS. Users complain.

You respond like most teams:

- Double app instances: 4 → 8.
- Calls per second to the DB also double.
- DB is now at 98% CPU, queueing requests, and latency gets worse.

You “scaled out”, but you poured fuel on the actual bottleneck.

Typical places this happens:

### 1. Single shared database

- All requests eventually funnel into one primary DB.
- Writes are serialized, transactions contend for the same rows/indexes.
- Read replicas help for reads, but writes still go through a single gate.

Scaling app nodes just means “more people trying to go through the same doorway”.

### 2. Locks and critical sections

- Global cache invalidation lock.
- A “leader” worker that must perform some part of the work.
- A single-node cron that does heavy aggregation.

Even if you have 50 workers, if they all wait on the same lock or single-worker step, you’ve effectively got a tiny serial section stuck in the middle of your “massively parallel” pipeline.

### 3. Chatty microservices

- Service A calls B, C, D sequentially.
- Each of those calls fans out to other services.
- Horizontal scaling just means more cross-service network calls flying around.

You might increase throughput, but latency becomes dominated by network trips, queues, and retries.

### 4. Stateful sessions

- In-memory sessions tied to one node.
- Caches that aren’t shared.
- User-specific state stuck to one instance.

You can add instances, but you’re forced into sticky sessions or complicated routing. Your effective capacity is lower than your instance count suggests.

---

## Amdahl’s Law: the “you can’t outrun the serial part” rule

Now for a simple mental model.

> Amdahl’s Law says your maximum speedup is limited by the part of the work that cannot be parallelized.

Imagine every request spends:

- 80% of time in parallelizable app logic and I/O.
- 20% in a single DB transaction that must run on one primary.

If you somehow make the parallel part infinitely fast (infinite app servers, magic CPUs), your speedup is capped at:

- Max speedup = **1 / 0.2 = 5×**

No matter how many instances you add, that 20% serial chunk puts a hard ceiling on your gains.

In real systems, “serial chunks” look like:

- A single primary database.
- A global mutex.
- A coordination service everyone calls (e.g., “config service”, “auth service”).
- A synchronous third-party API you must call.

Every big red box in your architecture diagram that everything talks to is an Amdahl bottleneck candidate.

---

**Before scaling:**

```text
[  Serial DB (200ms)  ][   Parallelizable app work (800ms)  ]  = 1000ms
```

**After “infinite” app scaling:**

```text
[  Serial DB (200ms)  ][ App work ~ 0ms ]  ≈ 200ms
```

Even with magic scaling, you can never go below the serial 200ms unless you change the architecture (e.g., denormalize, precompute, cache, or split the state).

---

## Gustafson’s Law: when more boxes do pay off

Amdahl is a bit pessimistic. Gustafson’s Law flips the perspective:

> Instead of “same work, less time”, ask: **“Same time, more work”** as you add resources.

This is much closer to how we actually scale systems:

- Analytics jobs: process more data overnight with more nodes.
- Stream processing: handle more events per second as you add workers.
- Multi-tenant SaaS: onboard more customers while keeping per-request latency acceptable.

Here, we’re okay if a single request still takes 200ms, as long as we can serve many more of them without the system collapsing.

Horizontal scaling shines when:

- The workload is naturally partitionable (per user, per tenant, per shard).
- Cross-partition coordination is minimal.
- You mostly care about throughput (“can we handle Black Friday?”) rather than shaving off the last 20ms of latency.

---

## Stateless vs stateful: where to actually scale

The most practical design heuristic for scalability is:

> **Scale stateless layers freely; design stateful layers carefully.**

### Stateless layer (your scaling playground)

Typical components:

- API gateways & load balancers
- Stateless web/API servers
- Job workers that pull tasks from a queue
- Edge functions / serverless handlers

Characteristics:

- No user-specific data stored in-process between requests.
- Can be killed, recreated, rescheduled anytime.
- Idempotent handlers + retries.

These are easy to scale horizontally: just add more replicas.

### Stateful layer (where complexity & bottlenecks live)

Typical components:

- Databases (SQL/NoSQL)
- Caches (Redis, Memcached)
- Message queues, logs (Kafka, RabbitMQ, SQS)
- File/Object storage (S3, GCS, etc.)

You scale these with:

- **Replication** – more read capacity, but writes still constrained.
- **Sharding/partitioning** – splitting data across nodes (by tenant, region, key).
- **CQRS and read models** – offload read-heavy paths to denormalized views.
- **Caching** – moving hot reads closer to the stateless tier.

Your real scalability work is here:  
moving from “one big shared thing” to “multiple smaller, partitioned, or specialized things”.

---

<img src="https://res.cloudinary.com/vannucherum/image/upload/v1763143875/vannucherum.com/posts/2025-11-15-scalability-101-horizontal-vs-vertical-and-where-the-bottlenecks-hide/3_wvrhwb.svg"/>

Scale the top box liberally. Treat the bottom box like a carefully planned garden.
