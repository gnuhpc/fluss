---
title: Fluss CAPE
sidebar_position: 10
---

# Fluss CAPE (Compatibility And Protocol Extensions)

**Fluss CAPE** is an external compatibility layer that transforms Apache Fluss into a multi-model database by adding **HBase**, **Redis**, **Kafka**, and **PostgreSQL** protocol compatibility.

## 🎯 What is Fluss CAPE?

Fluss CAPE enables existing applications to interact with Fluss using familiar protocols—without any modifications to the Fluss core. It operates as a stateless proxy layer that performs real-time protocol translation.

Key benefits:
- 🔌 **Zero Fluss Modifications** - Runs as a standalone translation layer.
- 🚀 **Instant Migration** - Use existing HBase/Redis/Kafka/PostgreSQL applications with Fluss.
- 🔄 **Unified Storage** - Access the same data through multiple protocols.

## 🏗️ Core Principles

### Protocol Translation Architecture
CAPE operates as a stateless proxy:
1. **Decode**: Receives requests via standard protocol handlers (HBase RPC, Redis RESP, Kafka Wire, PG Wire).
2. **Translate**: Maps protocol-specific operations (e.g., `HSET`, `Put`, `Produce`) to Fluss native table operations.
3. **Execute**: Uses the high-performance Fluss Client to interact with the underlying distributed storage.

### Log vs. KV Tables in CAPE
Fluss provides two primary table types, both of which are leveraged by CAPE:
- **KV Tables (Primary Key Tables)**: Used primarily for **HBase** and **Redis**. Optimized for low-latency point lookups and range scans.
- **Log Tables**: Used primarily for the **Kafka protocol**. Optimized for high-throughput append-only ingestion and sequential consumption.
- **Hybrid Support**: The **PostgreSQL protocol** primarily operates on Primary Key Tables but leverages both the KV component (for snapshots) and Log component (for real-time changelog replay) to ensure consistent results.

## 🌊 Lake-Stream Integration (湖流一体)
Fluss CAPE fully inherits and extends Fluss's "Lake-Stream Integration" architecture:
- **Unified Messaging & Storage**: Bridges Fluss changelogs and Kafka topics seamlessly. Mutations in HBase or Redis tables are automatically captured as changelogs, which can be consumed via the Kafka protocol in real-time.
- **Unified Interface**: Write data via a "streaming" protocol (Kafka) and immediately query it via a "database" protocol (PostgreSQL/HBase/Redis).

## 🚀 Getting Started

Fluss CAPE is maintained as a separate component. To get started, please refer to the [Fluss CAPE Repository](https://github.com/gnuhpc/fluss-cape).
