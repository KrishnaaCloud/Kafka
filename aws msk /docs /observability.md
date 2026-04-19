# Observability & Management Layer

## AKHQ (Kafka Operations UI)
To avoid manual CLI-based monitoring, I managed the deployment of **AKHQ** as our primary visual operations dashboard.

### Key Capabilities:
- **Topic Exploration**: Real-time view of message contents and partition distribution.
- **Consumer Group Monitoring**: Visual tracking of "Lag" to ensure Airflow teams are keeping up with the MSK ingestion.
- **Node Health**: Direct visibility into the health and synchronization of the three MSK brokers.

---

## Kafka REST Proxy
I implemented the **Confluent REST Proxy** to bridge the gap between our MSK cluster and non-native Kafka applications within the organization.

### Why we included it:
- **HTTP Connectivity**: Allows lightweight web applications or legacy systems to produce/consume data via standard HTTP calls without needing complex Kafka drivers.
- **Metadata Access**: Provides a unified API for retrieving cluster information, topic lists, and partition offsets.

---

## Tooling Architecture Diagram

```mermaid
graph TD
    A[MSK Broker Cluster] --> B[AKHQ Dashboard]
    A --> C[Kafka Connect Worker]
    A --> D[Kafka REST Proxy]
    
    E[DevOps Team] -->|Monitor Lag| B
    F[Legacy Web Apps] -->|HTTP Produce| D
    G[Consumer Teams] -->|Verify Data| B
