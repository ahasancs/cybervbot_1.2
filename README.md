# SIEM+SOAR Ransomware Detection PoC
This repository is a GitHub-ready starter template for a SIEM + SOAR platform
integrating flow-based ML ransomware detection, SDN-driven quarantine, and a SOC dashboard.

## Contents
- docker-compose.yml: simplified PoC composition (Kafka, Zookeeper, ES, Kibana, model scoring service)
- services/collector/producer.py: sample Kafka producer that emits flow events (JSON)
- services/model-scoring/app.py: FastAPI + ONNX scoring endpoint
- services/model-scoring/Dockerfile: Dockerfile for scoring service
- schemas/FlowEvent.avsc, EnrichedFlow.avsc: Avro schemas
- playbooks/ransomware_quarantine.yaml: SOAR playbook example
- sdn/ryu_app.py: Ryu controller PoC for blocking IPs via OpenFlow
- dashboards/: simple static HTML mockups for SOC UI
- docs/architecture.mmd: Mermaid diagram
- LICENSE: MIT
- CONTRIBUTING.md: how to run the PoC locally

## Quickstart (local PoC)
1. Install Docker & Docker Compose.
2. Put a small ONNX model in `onnx_models/rf_model.onnx` or leave placeholder.
3. From repo root:
   ```bash
   docker-compose up --build
   ```
4. Start the collector to produce events (services/collector/producer.py).
5. Use the scoring endpoint: `curl -X POST http://localhost:8000/score -d '{"flow_id":"1","features":[0.1,0.2]}'`

## Notes
- This PoC uses JSON for simplicity. In production use Avro/Schema Registry for throughput & compatibility.
- See docs/ for architecture details and deployment guidance.
