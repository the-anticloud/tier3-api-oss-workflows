# L5 Narrow / L2 General Classification — api-oss-workflows
**Platform:** Anticloud | **PAX:** 27B | **IP:** USPTO pending 2026, Anticloud FZ LLE
**Domain:** Sovereign workflow engine: DAG-based pipelines for multi-step Anticloud operations

## L5 Narrow
api-oss-workflows specializes in sovereign workflow engine: dag-based pipelines for multi-step anticloud operations within the Anticloud sovereign deployment boundary. All operations stay local — no cloud services, no external APIs, no data exfiltration. The narrow scope ensures deterministic, auditable behavior that PAX 27B can reason about precisely.

## L2 General
L2 General means api-oss-workflows is available to all 9 Anticloud tiers without per-tier configuration. The same API serves hospital, defense, robotics, and research deployments.

## PAX Integration
PAX 27B is used for workflow generation: describe a multi-step operation in natural language and PAX generates the DAG definition with appropriate task types and dependencies.

## AIOSS Audit Relevance
Every workflow execution (workflow ID + DAG hash + step completion hashes + final output hash) is AIOSS-chained: H_n = SHA3-256(H_{n-1} || entry_hash_n || timestamp_n).
Tamper-evident, offline-verifiable, zero cloud dependency.

## Regulatory / Compliance
IEC 61508 (safety-critical workflows), NIST SP 800-53 SA-8 (engineering processes)
