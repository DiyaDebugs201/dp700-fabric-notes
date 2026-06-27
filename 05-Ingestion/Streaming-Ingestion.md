-# Streaming Ingestion

## What is Streaming Ingestion?

Streaming ingestion is the process of collecting and processing data continuously as it is generated.

Unlike batch ingestion, data is processed almost immediately instead of waiting for a scheduled job.

Think:

> A live news broadcast—you receive updates as events happen, not at the end of the day.

---

# Why Use Streaming?

Some applications require immediate insights.

Examples:

* Fraud detection
* IoT sensor monitoring
* Website click tracking
* Stock market analysis
* Live GPS tracking
* Social media feeds

In these scenarios, waiting hours for a batch job is not acceptable.

---

# Streaming Workflow

Event Source
↓
Eventstream
↓
Real-Time Intelligence
↓
KQL / Eventhouse
↓
Dashboards & Alerts

---

# Characteristics

* Continuous data flow
* Very low latency
* Near real-time processing
* Immediate analytics
* Supports event-driven architectures

---

# Common Streaming Data Sources

Examples:

* IoT devices
* Mobile applications
* Web applications
* Sensors
* Payment systems
* Log files
* Clickstream data

---

# Streaming Components in Microsoft Fabric

## Eventstream

Used to:

* Collect streaming events
* Route data
* Filter events
* Transform events

Acts as the entry point for streaming data.

---

## Eventhouse

Stores large volumes of streaming data.

Optimized for:

* Fast ingestion
* Real-time analytics
* KQL queries

---

## KQL (Kusto Query Language)

Used to query streaming and telemetry data.

Common operations:

* Filtering
* Aggregation
* Time-based analysis
* Event investigation

---

## Spark Structured Streaming

Allows Spark to process continuous streams of data.

Useful for:

* Large-scale stream processing
* Real-time transformations
* Machine learning pipelines

---

# Native Tables vs OneLake Shortcuts

In Real-Time Intelligence, data can be accessed through:

### Native Tables

Data is stored directly in Eventhouse.

Advantages:

* Fastest query performance
* Best for frequently accessed streaming data

---

### OneLake Shortcuts

Reference data stored elsewhere without copying it.

Advantages:

* No data duplication
* Lower storage costs
* Easy integration with existing datasets

---

# Query Acceleration for OneLake Shortcuts

Fabric can accelerate queries on shortcut data.

Benefits:

* Faster analytics
* Reduced latency
* Better performance on external datasets

---

# Windowing Functions

Streaming data is often analyzed over time windows.

Common windows:

### Tumbling Window

Fixed, non-overlapping time intervals.

Example:

Count website visits every 5 minutes.

---

### Sliding Window

Overlapping windows that move continuously.

Example:

Average temperature over the last 10 minutes, updated every minute.

---

### Session Window

Groups events based on user activity.

Example:

Track a user's shopping session until they are inactive.

---

# Batch vs Streaming

| Feature      | Batch         | Streaming         |
| ------------ | ------------- | ----------------- |
| Processing   | Scheduled     | Continuous        |
| Latency      | Minutes/Hours | Seconds           |
| Data Arrival | Groups        | Individual Events |
| Best For     | Reports       | Live Analytics    |
| Example      | Payroll       | Fraud Detection   |

---

# Common Streaming Use Cases

### Fraud Detection

Detect suspicious transactions immediately.

---

### IoT Monitoring

Monitor sensor data continuously.

---

### Live Dashboards

Display current business metrics.

---

### Log Analytics

Analyze application logs in real time.

---

### Traffic Monitoring

Track vehicles or deliveries live.

---

# Common DP-700 Scenarios

### Scenario 1

Requirement:

Analyze website clicks as users browse.

Answer:

Streaming Ingestion.

---

### Scenario 2

Requirement:

Monitor factory sensors continuously.

Answer:

Eventstream + Eventhouse.

---

### Scenario 3

Requirement:

Query millions of streaming events.

Answer:

KQL.

---

### Scenario 4

Requirement:

Need Spark for continuous data processing.

Answer:

Spark Structured Streaming.

---

# Common Exam Traps

### Trap 1

Question:

Is streaming always faster than batch?

Answer:

Streaming provides lower latency but is generally more complex and can cost more.

---

### Trap 2

Question:

Which Fabric component ingests streaming events?

Answer:

Eventstream.

---

### Trap 3

Question:

Which query language is commonly used for Eventhouse?

Answer:

KQL.

---

### Trap 4

Question:

Can OneLake Shortcuts be used with Real-Time Intelligence?

Answer:

Yes.

---

# Memory Tricks

Batch

= Netflix Download

Watch later.

---

Streaming

= YouTube Live

Watch immediately.

---

Eventstream

= Highway carrying live events.

---

Eventhouse

= Warehouse storing streaming events.

---

KQL

= SQL for telemetry and streaming data.

---