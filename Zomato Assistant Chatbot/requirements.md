# Zomato Assistant Chatbot

## Functional Requirements

1. User can raise the complaint through chatbot after selected categories.
2. User can decribe thier issue, upload images and ask for resolution.
3. Chatbot will try to solve issue, else forward it to human.

## Non Functional Requirements

1. Availability while creating a complaint.
2. Consistency during chat.

## Scale

Average QPS : 100K * 5 Messages/s = 500k QPS
Peek QPS : 2M QPS
Size : 500K * 100KB * 10 = 5TB for 10 days. Storing chat for at max 10 days

## APIs

Create Complaint : POST api/v1/orders/{orderId}/complaint
Fetch Complaint : GET api/v1/complaints/{complaintId}
Chat : wss:://zomato.chat.api/{complaintId}/chat

## Data Model

1. Complaints
    - complaintId
    - orderId
    - userId
    - category
    - description
    - status

2. Messages
    - messageId
    - chatId
    - complaintId

3. Chats
    - complaintId
    - userId

4. Users
    - userId
    - orderId
