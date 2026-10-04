# Discord

## Functional Requirements

1. User can join public server and private server via invites.
2. User can create public and private server and invite other users to private server.
3. User can chat, voice call and video call to other users.
4. Within a server user can chat, call and stream.
5. User can send file, images, link and stickers in the chat.

## Non Functional Requirements

1. Consistency during chat sessions.
2. Availability during video, voice call sessions.
3. Latency of 200ms for chat, low latency for voice and video call.

## Scale

1. Chat: 2M DAU * 1000 Messages/day = 20000 messages/ s, peek = 60000 messages/s
2. Size : 2M * 1000 * 10MB * 400 = 10TB for 1Year -> 50PB.

## APIs

1. Join Public Server: POST /v1/server/members
2. Create Private Server Invite: POST /v1/server/invites
3. Join Private Server: POST /v1/server/invited_members
4. Start Streaming: POST /v1/server/channel/streams
5. Chatting: wss:://gateway.discord/channel 

## Entities

1. User
2. Server
3. Channel
4. Messages
5. Metadata

## Data Model

1. User : userId, email, followers, username
2. Server : serverId, ownerId, name, visiblity
3. ServerMembers : serverId, userId, role, joinedAt
4. Channel : channelId, serverId, type, name
5. Invite : inviteId, serverId, createdBy, expiresAt
6. Messages : messageId, channelId, userId, content, createdAt, metadataId
7. Metadata : metadataId, mesaageId, link
