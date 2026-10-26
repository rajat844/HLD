# Event Forwarding Platform

## Functional Requirements

1. Client apps and backend services can publish raw events, the system validates payloads against registered schemas.
2. The system can filter out unneeded events, enrich payloads with missing dimensions and restructure payloads to match destination formats.
3. Services can subscribe to specific event types, define routing rules, and register expected destination payload structures.
4. Undelivered events are quarantined into a DLQ with support for manual replay.

## Non Functional Requirements

1. High Availability while receiving the events and buffer sudden traffic bursts without dropping events.
2. High Consistency and imdepotency while forewarding the events.
3. A slow downstream destination must not block event forwarding to heathy destination.
4. System will be highly durable.

## Scale

1. Average Ingestion : 10K apps * 100K events per day -> 10000 QPS
2. Peek Ingestion : 50000 QPS
3. Average Delivery : 10000 Q * 10 services -> 10 ^ 5 Deliveries/s
4. Peek Delivery : 5 * 10 ^ 5 Deliveries/s
5. Storage : 10K apps * 10 rules * 5KB = 500MB

## Entities

1. client
    - clientId

2. EventSchema
    - schemaId
    - clientId
    - eventType
    - JsonSchema

3. Destination Services
    - servicesId
    - clientId
    - destinationType
    - url
    - eventType
    - routingRules
    - transformationTemplete

4. event
    - eventId
    - clientId
    - eventType
    - timestamp
    = payload

## APIs

1. Registering Client : POST /v1/api/eventSchema -> {clientId, eventType, jsonSchema }
2. Registering Services : POST /v1/api/services -> {clientId, serviceId,destinationType,  url, eventType. routingRules, transformationTemplate}
3. Events : POST /v1/api/events -> {clientId, eventId, evntType, timestamp, payload}