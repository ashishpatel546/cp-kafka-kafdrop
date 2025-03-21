# Kafka Setup with Docker Compose

This setup provides a complete Kafka environment with multiple services for development and monitoring.

## Services and Ports

| Service         | Port  | Description                                  |
| --------------- | ----- | -------------------------------------------- |
| Kafka           | 29092 | Main Kafka broker (accessible via localhost) |
| Schema Registry | 8081  | Schema Registry UI and API                   |
| Control Center  | 9021  | Confluent Control Center web interface       |
| Kafdrop         | 9000  | Kafka web UI for topic management            |

## Available Services

### 1. Zookeeper

- Manages Kafka cluster coordination
- Internal port: 2181

### 2. Kafka Broker

- Main message broker service
- External port: 29092 (for local connections)
- Internal port: 9092 (for container communications)

### 3. Schema Registry

- Manages Avro schemas
- Access UI at: http://localhost:8081

### 4. Confluent Control Center

- Advanced monitoring and management interface
- Access UI at: http://localhost:9021

### 5. Kafdrop

- Light-weight Kafka UI
- Access UI at: http://localhost:9000

## Getting Started

1. Start all services:

```bash
docker-compose up -d
```

2. Stop all services:

```bash
docker-compose down
```

3. View logs:

```bash
docker-compose logs -f [service-name]
```

## Important Notes

- Kafka is configured with auto topic creation disabled
- Single broker setup with replication factor of 1 (suitable for development)
- Schema Registry is required for Avro message serialization/deserialization
- You can access Kafka from your local machine at `localhost:29092`
- For services within Docker, use `kafka:9092` as the broker address

## Alternative UI

The docker-compose file includes a commented section for Redpanda Console (on port 8080) as an alternative to Kafdrop. To use it:

1. Comment out the Kafdrop service
2. Uncomment the Redpanda Console service
3. Restart the stack
