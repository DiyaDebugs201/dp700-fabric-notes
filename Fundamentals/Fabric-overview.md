# Microsoft Fabric Overview

## What is Microsoft Fabric?

Microsoft Fabric is a unified analytics platform that combines data engineering, data integration, data warehousing, data science, real-time analytics, and business intelligence into a single Software-as-a-Service (SaaS) platform.

Instead of using multiple separate services, Fabric provides a single environment where data professionals can store, process, analyze, and visualize data.

---

## Why was Fabric Created?

Traditionally, organizations used different tools for:

* Data storage
* Data engineering
* Data transformation
* Data warehousing
* Reporting
* Data science

Managing multiple tools increased complexity and operational overhead.

Fabric solves this problem by providing:

* One platform
* One storage layer
* One security model
* One user experience

---

## Core Components of Fabric

### OneLake

The centralized storage layer of Microsoft Fabric.

Think of OneLake as:

> OneDrive for organizational data.

All Fabric workloads use OneLake as the underlying storage system.

---

### Lakehouse

Combines capabilities of:

* Data Lake
* Data Warehouse

Supports:

* Structured data
* Semi-structured data
* Unstructured data

Optimized for Spark workloads and Delta tables.

---

### Data Warehouse

Provides:

* Relational storage
* Full T-SQL support
* BI reporting
* Analytical workloads

Best for SQL-centric teams.

---

### Data Engineering

Supports:

* Spark
* Notebooks
* Data Pipelines
* Data Transformation

Used to ingest and prepare data.

---

### Real-Time Intelligence

Used for:

* Streaming data
* Event processing
* Near real-time analytics

Common examples:

* IoT devices
* Application logs
* Sensor data

---

### Power BI

Used for:

* Dashboards
* Reports
* Business analytics
* Data visualization

Integrated directly into Fabric.

---

## Fabric Workspace

A workspace is a logical container used to organize Fabric items.

A workspace can contain:

* Lakehouses
* Warehouses
* Pipelines
* Notebooks
* Reports
* Semantic Models

Think of a workspace as:

> A project folder containing all resources related to a business solution.

---

## Fabric Item Hierarchy

Tenant
→ Domain
→ Workspace
→ Items

Examples of items:

* Lakehouse
* Warehouse
* Notebook
* Pipeline
* Semantic Model
* Report

---

## Capacity and SKUs

Fabric uses Capacity Units (CU) to provide compute resources.

Organizations purchase Fabric capacity using SKUs.

Examples:

* F2
* F4
* F8
* F16
* F32
* F64

Higher SKUs provide more compute capacity.

---

## Important Capacity Concepts

### Bursting

Allows workloads to temporarily consume more resources than their baseline allocation.

Useful during sudden workload spikes.

---

### Smoothing

Distributes resource consumption over time to prevent sudden performance issues.

---

### Throttling

Occurs when capacity limits are exceeded.

Fabric may slow or delay workloads to protect system stability.

---

### Autoscale

Automatically adjusts available capacity when workload demands increase.

---

## Why Fabric is Important for Data Engineers

A Data Engineer uses Fabric to:

* Ingest data
* Transform data
* Store data
* Secure data
* Monitor data pipelines
* Optimize performance

Fabric provides all required tools within one ecosystem.

---

## DP-700 Exam Focus

Know:

* What Fabric is
* Why Fabric exists
* Workspace structure
* Fabric items
* OneLake's role
* Capacity concepts
* Differences between Lakehouse and Warehouse

These topics appear frequently in scenario-based questions.

---

## Quick Revision

* Fabric is an end-to-end analytics platform.
* OneLake is the central storage layer.
* Workspace contains Fabric items.
* Lakehouse combines Data Lake and Warehouse concepts.
* Warehouse is optimized for SQL analytics.
* Capacity is measured using CUs.
* Bursting handles temporary spikes.
* Smoothing spreads usage over time.
* Throttling occurs when limits are exceeded.
* Autoscale increases capacity when needed.
