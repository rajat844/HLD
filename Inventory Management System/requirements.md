# Inventory Management System

## Functional Requirements

1. User can view real-time item availability based on location
2. User can reserve the stock on checkout, commit on payment or release it back on failure.
3. User can subscribe to out-of-stock items alert and will be notified when item is back in stock.
4. Admin can add items to the stock, confiure the threshold for each item and get notified whenever the item is below threshold.

## Non Functional Requirements

1. High Availability and low latency for reads.
2. Consistency at checkout
3. Unpaid reserved stock will automatically released.

## Scale

1. Average Queries for item availability: 100M DAU * 100 Queries a day = 100K QPS
2. Peek : 500K QPS
3. Average Queries for item checkout: 100M DAU * 10 = 10K QPS
4. Peek : 50K QPS
5. Database: 100M items * 1Kb = 100GB

## Entities

1. Inventory
   - itemId(PK)
   - location(PK)
   - quantity
   - threshold

2. User
    - userId (PK)
    - role

3. Notification
    - notificationId
    - userId (PK)
    - itemId
    - location
    - type

4. Reserved
    - reservationId(PK)
    - itemId
    - userId
    - quantity
    - location
    - createdAt
    - expiringAt
    - status

## APIs

1. Getting the stock : GET /v1/api/inventory/{itemId}?location={location}
2. Chekout : POST /v1/api/reserved
        Body : {reservationId, itemId, userId, location, quantity}
3. Update Status : UPDATE /v1/api/reserved/{reservationId}
        Body : {status}
4. Notification Subsciption : POST /v1/api/notification
        Body : {notificationId, userId, itemId, location, type}
5. Refilling Stock : POST /v1/api/invertory/
        Body : {itemId, locationId, quanitity}
6. Update Threshold : UPDATE /v1/api/inventory/{itemId}
        Body : {location,threshold}
