# Log Monitoring System

## Requirements

1. Client services can continously push structured or unstructured logs to the System.
2. User can query and view logs filtered by time window, service name, severity-level and full-text search within 15 days.
3. User can define custom alert rules and configure notification channels.
4. User can configure retention policy per service or log level.

## Non Functional Requirements

1. Low end to end latency.
2. High ingestion availability and spike tolerance.
3. Zero data loss for ingested error and fatal logs.
4. Minimum Client Overhead.
5. High scalability.

## Scale

1. Log Ingestion: 100 services * 100 hosts * 1 (100 log lines per second- batched in one) = 10^ 4 qps
2. Peek Log Ingestion = 5 * 10 ^ 4 qps
3. Storage : 100 services * 100 hosts *  100KB(log size a second) * 10^5 * 400 = 40PB.

## Entities

- owner
  - ownerId

- services
  - serviceId
  - ownerId
  - retention days

- logs
  - logId
  - serviceId
  - timestamp
  - logLevel
  - message
  - hostId

- notification
  - notificationId
  - serviceId
  - notification channel
  - notification target
  - alertCondition

## APIs

1. Ingestion : POST/v1/api/logs/{logId}
    - Body : {serviceId, hostId, logs: [{timestamp, logLevel, message}]}
2. Search : GET /v1/api/logs?{keyword}&level={level}&service={serviceId}&timeWindow={timeWindow}&limit=50
3. Get Log : GET /v1/api/logs/{logId}
4. Notification : POST /v1/api/notification
    - Body : {serviceId, alertCondition, channel, url}
5. Service Registration : POST /v1/api/Services
    - Body : {serviceId, ownerId, retentionDays}
