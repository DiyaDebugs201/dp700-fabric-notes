# Batch Ingestion

## What is Batch Ingestion?

Batch ingestion is the process of collecting and loading data into an analytics platform in scheduled groups (batches) instead of processing each record immediately.

Data is accumulated over a period of time and then processed together.

Think:

> Instead of delivering one letter at a time, the post office delivers an entire bag of letters at once.

---

# Why Use Batch Ingestion?

Many business processes do not require real-time updates.

Examples:

* Daily sales reports
* Payroll processing
* Monthly financial reports
* Inventory synchronization
* Customer database updates

Processing data in batches is often simpler and more cost-effective.

---

# Batch Ingestion Workflow

Source Systems
↓
Extract Data
↓
Pipeline / Dataflow
↓
Lakehouse / Warehouse
↓
Transformation
↓
Analytics

---

# Characteristics of Batch Processing

* Processes data at scheduled intervals.
* Handles large volumes of data.
* Higher latency compared to streaming.
* Easier to manage and monitor.
* More cost-efficient for non-real-time workloads.

---

# Common Batch Data Sources

Examples include:

* SQL Server
* Azure SQL Database
* CSV files
* Excel files
* REST APIs
* ERP systems
* CRM systems

---

# Batch Processing in Microsoft Fabric

Common Fabric components:

### Data Pipelines

Used to:

* Copy data
* Schedule ingestion
* Automate workflows

---

### Dataflows Gen2

Used for:

* Low-code data transformation
* Data preparation
* Business-friendly ingestion

---

### Spark Notebooks

Used for:

* Large-scale transformations
* Data cleansing
* Machine learning preparation

---

# Scheduling Batch Jobs

Batch ingestion is commonly scheduled:

* Every hour
* Daily
* Weekly
* Monthly

Example:

Every day at 2:00 AM

↓

Load previous day's sales data

↓

Transform

↓

Update reporting tables

---

# Full Load vs Incremental Load

## Full Load

Loads all available data every time.

Advantages:

* Simple implementation
* Easy to understand

Disadvantages:

* Slow for large datasets
* Higher compute costs

Example:

Load all customer records every night.

---

## Incremental Load

Loads only new or changed data.

Advantages:

* Faster
* Lower cost
* Better scalability

Disadvantages:

* More complex implementation

Example:

Load only today's new sales transactions.

---

# Typical Batch Transformations

After ingestion, common operations include:

* Remove duplicates
* Handle null values
* Join datasets
* Filter records
* Aggregate data
* Standardize formats
* Validate business rules

---

# Batch Ingestion Example

Scenario:

A retail company stores sales transactions in a SQL database.

Every midnight:

1. Copy new sales data.
2. Store it in a Lakehouse.
3. Clean the data.
4. Update Gold tables.
5. Refresh Power BI reports.

No real-time processing is required.

---

# Advantages

* Simpler architecture
* Predictable execution
* Lower operational cost
* Efficient for large datasets
* Easier troubleshooting

---

# Limitations

* Higher latency
* Reports are not real-time
* Delayed business insights
* Large failures may require rerunning the batch

---

# Batch vs Real-Time

| Feature    | Batch            | Real-Time            |
| ---------- | ---------------- | -------------------- |
| Processing | Scheduled        | Continuous           |
| Latency    | Minutes to Hours | Seconds              |
| Cost       | Lower            | Higher               |
| Complexity | Lower            | Higher               |
| Example    | Payroll          | Live Fraud Detection |

---

# Common DP-700 Scenarios

### Scenario 1

Requirement:

Daily sales data needs to be loaded every night.

Solution:

Batch Ingestion.

---

### Scenario 2

Requirement:

Large historical data migration.

Solution:

Batch Processing.

---

### Scenario 3

Requirement:

Monthly financial reporting.

Solution:

Batch Ingestion.

---

### Scenario 4

Requirement:

Process millions of records every weekend.

Solution:

Batch Processing with Spark or Pipelines.

---

# Common Exam Traps

### Trap 1

Question:

Does batch processing mean slow processing?

Answer:

No.

It means scheduled processing.

---

### Trap 2

Question:

Which loading pattern is more efficient for large historical datasets?

Answer:

Batch.

---

### Trap 3

Question:

Which Fabric components commonly support batch ingestion?

Answer:

* Data Pipelines
* Dataflows Gen2
* Spark Notebooks

---

# Memory Trick

Batch

= School Bus

Everyone travels together.

---

Streaming

= Taxi

Every passenger travels immediately.

---