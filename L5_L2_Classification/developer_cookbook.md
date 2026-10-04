# Developer Cookbook — api-oss-workflows
**Stack:** Python 3.11, asyncio, networkx (DAG), AIOSS_FORMAT
**Domain:** Sovereign workflow engine: DAG-based pipelines for multi-step Anticloud operations
**License:** Apache-2.0 | **IP:** USPTO pending 2026, Anticloud FZ LLE

## Core Usage

```python
from api_oss_workflows import WorkflowEngine, Task
engine = WorkflowEngine(aioss_chain='./workflows.aioss')

# Define DAG
@engine.workflow
def clinical_audit_pipeline():
    ingest = Task('api-oss-data', 'ingest', source='./clinical_records.csv')
    transform = Task('api-oss-data', 'transform', depends_on=[ingest])
    audit = Task('api-oss-compliance', 'generate', framework='HIPAA', depends_on=[transform])
    notify = Task('api-oss-webhooks', 'dispatch', event='audit.complete', depends_on=[audit])
    return [ingest, transform, audit, notify]

result = await engine.run(clinical_audit_pipeline)
print(f'Workflow complete: {result.chain_hash}')
```

## AIOSS Chain Append

```python
import hashlib, time

def aioss_append(chain_path, payload: bytes, module_id: str):
    entry_hash = hashlib.sha3_256(payload).digest()
    ts = int(time.time_ns()).to_bytes(8, 'big')
    with open(chain_path, 'rb') as f:
        f.seek(-32, 2); prev_hash = f.read(32)
    new_hash = hashlib.sha3_256(prev_hash + entry_hash + ts).digest()
    with open(chain_path, 'ab') as f:
        f.write(ts + entry_hash + new_hash)
    return new_hash.hex()

# After every api-oss-workflows output:
chain_hash = aioss_append("./api_oss_workflows.aioss",
                           result_bytes, "api-oss-workflows")
```

## Performance & Integration

Performance: profile with api-oss-devtools. Benchmark with api-oss-analytics. Integration: all api-oss-workflows operations are logged to api-oss-logging and audited by api-oss-compliance.
