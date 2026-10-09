# Webhook Delivery Platform

## Functional Requirements

1. User can register and deregister the endpoint to receive webhook event.
2. User can subscribe their service to specif event types.
3. When an event is generated the platform should update all registered services.
4. Platform should be able to confirm whether event was successfully delivered or not.

## Non Functional Requirements

1. CAP Theorum : Availability while registering endpoints, receiving updates from services.
2. Retry the event delivery: Follow gaurantee minimum one delivery.
3. Retries should be idempotent.
4. Failed events to be added to DLQs.

## Scale

1. Average Traffic : 100K DAU * 100 events/ day = 10M / 10 ^ 5 = 100qps
2. Peek Traffic : 5 * 100 qps
3. Storage : 1 event = 1KB = 10M * 300 = 3TB/year

## APIs

1. Register Endpoints : POST /v1/endpoint/{user}
2. Register Event Type : POST /v1/event/{user}
3. Register Endpoints to Events: POST /v1/subscriptions/

## DATA MODEL

1. Endpoints
    - endpointId
    - userId
    - url

2. EventsType
    - eventId
    - userId
    - event

3. Subscription
    - userId
    - eventId
    - subscriber

4. User
    - userId
