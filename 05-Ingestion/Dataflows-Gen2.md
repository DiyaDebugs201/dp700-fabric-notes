# Dataflows Gen2

## What is Dataflows Gen2?

Dataflows Gen2 is a low-code/no-code data ingestion and transformation tool in Microsoft Fabric.

It allows users to connect to multiple data sources, clean and transform data using a visual interface, and load the results into Fabric destinations such as a Lakehouse or Warehouse.

Think:

> **Power Query for Data Engineering.**

---

# Why Use Dataflows Gen2?

Not every data engineer or analyst wants to write PySpark or SQL.

Dataflows Gen2 provides a visual way to:

* Connect to data sources
* Clean data
* Transform data
* Load data into Fabric

without writing much code.

---

# Dataflow Gen2 Workflow

Data Source

↓

Connect

↓

Power Query Transformations

↓

Preview Results

↓

Load to Lakehouse / Warehouse

---

# Main Features

## Multiple Connectors

Supports connections to:

* SQL Server
* Azure SQL Database
* Excel
* CSV
* SharePoint
* REST APIs
* Azure Blob Storage
* OneLake
* Many other cloud and on-premises sources

---

## Visual Data Transformation

Common transformations include:

* Rename columns
* Remove duplicates
* Filter rows
* Sort data
* Merge queries
* Split columns
* Change data types
* Replace values

All through a graphical interface.

---

## Power Query Engine

Dataflows Gen2 uses the **Power Query** engine and **Power Query M** language behind the scenes.

Most transformations are created visually, but advanced users can edit the generated M code if needed.

---

## Loading Destinations

Data can be loaded into:

* Lakehouse
* Warehouse
* Other supported Fabric destinations

---

# Dataflows Gen2 vs Notebook vs Pipeline

| Feature             | Dataflow Gen2 | Notebook                | Pipeline                    |
| ------------------- | ------------- | ----------------------- | --------------------------- |
| Coding Required     | Very Little   | Yes                     | No (mostly configuration)   |
| Best For            | Data Cleaning | Complex Transformations | Workflow Orchestration      |
| Uses Spark          | No            | Yes                     | Can execute Spark notebooks |
| Visual Interface    | Yes           | No                      | Yes                         |
| Supports Scheduling | Yes           | Through orchestration   | Yes                         |

---

# When Should You Use Dataflows Gen2?

Choose Dataflows Gen2 when:

* You need a low-code solution.
* Data transformations are relatively simple.
* Business analysts or citizen developers are involved.
* You are familiar with Power Query.

Examples:

* Cleaning Excel data.
* Combining CSV files.
* Removing duplicates.
* Changing data types.

---

# When Should You Use a Notebook?

Choose a Notebook when:

* Working with very large datasets.
* Using PySpark or SQL.
* Building machine learning pipelines.
* Performing advanced transformations.
* Implementing custom logic.

---

# When Should You Use a Pipeline?

Choose a Pipeline when:

* Orchestrating multiple tasks.
* Scheduling workflows.
* Running notebooks.
* Copying data between systems.
* Building end-to-end data workflows.

---

# Common Dataflow Transformations

Examples include:

* Remove duplicate rows
* Handle NULL values
* Merge datasets
* Append datasets
* Rename columns
* Split columns
* Change data types
* Filter unwanted records
* Aggregate data

---

# Typical Dataflow Process

Sales CSV

↓

Remove duplicates

↓

Convert Date column

↓

Replace NULL values

↓

Load into Bronze Lakehouse

---

# Advantages

* Low-code development
* Easy to learn
* Rich connector library
* Visual debugging
* Quick data preparation
* Tight integration with Fabric

---

# Limitations

* Less flexible than Spark notebooks
* Not ideal for very complex logic
* Limited customization compared to code-based solutions

---

# Dataflows in ELT

Dataflows Gen2 fits naturally into the ELT pattern.

Extract

↓

Load into Fabric

↓

Transform using Power Query

↓

Store in Lakehouse or Warehouse

---

# Common DP-700 Scenarios

### Scenario 1

Requirement:

A business analyst needs to clean Excel data without writing code.

Answer:

Dataflows Gen2.

---

### Scenario 2

Requirement:

Transform millions of records using PySpark.

Answer:

Notebook.

---

### Scenario 3

Requirement:

Schedule multiple ingestion tasks every night.

Answer:

Pipeline.

---

### Scenario 4

Requirement:

Merge CSV files from SharePoint using a visual interface.

Answer:

Dataflows Gen2.

---

# Common Exam Traps

### Trap 1

Question:

Does Dataflows Gen2 require Spark programming?

Answer:

No.

It uses Power Query.

---

### Trap 2

Question:

Which tool is best for visual data transformation?

Answer:

Dataflows Gen2.

---

### Trap 3

Question:

Which tool should you use for complex PySpark transformations?

Answer:

Notebook.

---

### Trap 4

Question:

Which Fabric component is responsible for orchestration?

Answer:

Pipeline.

---

# Memory Tricks

Dataflow Gen2

= Excel + Power Query on steroids.

---

Notebook

= Python Developer.

---

Pipeline

= Project Manager.

Coordinates everyone's work.

---
