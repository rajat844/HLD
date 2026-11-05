# Gmail

## Functional Requirements

1. User can create a account with a unique username check.
2. User can send, receive, reply, foreward, emails with support for attachments, cc and bcc.
3. Unsent compositions are automatically and continously saved as drafts.
4. Mails are automatically grouped into threaded conversations can user can organize them with system or custom labels
5. User can search through their message history instantly by keywords, sender, date or attachments.

## Non Functional Requirements

1. CAP Theorum: High Availability over strong consistency.
2. Core UI interactions must complete in 1-2 seconds.
3. High durability.

## Scale

1. Average Traffic : 1B User * 10 mails a day = 10^5 QPS
2. Peek Traffic: 5 * 10^5 QPS
3. Storage: 10 KB * 1B * 10 * 365 = 400 PB/Year

## Entities

1. User
    - userId
    - userName
    - createdAt

2. Thread
    - threadId
    - subject
    - lastMessage

3. Mail
    - mailId
    - threadId
    - senderId
    - recipientList
    - attachments Metadata
    - createdAt
    - subject
    - body
    - isDraft

4. Labels
    - labelId
    - labelName
    - userId
    - threadId

## APIs

1. Create Account : POST /v1/api/user -> {userId, userName}
2. Send Mail/ Save to Draft :  POST /v1/api/mail -> {senderId, [recipients], subject, body, atatchmentsMetadata, isDraft}
3. Get Mails : GET /v1/api/threads?userId={userId}
4. Create Labels : POST/ v1/api/label -> {labelId, labelName, userId,maidId}
5. Get Inbox : GET /v1/api/thread?userId={userId}&label={labelId}