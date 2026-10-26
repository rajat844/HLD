# Configuration Management System

## Functional Requirements

1. User can update configurations on one device, and other active devices will automatically receive and update the configurations in real time.
2. User can modify configurations while offline, changes will batched locally and will sync once user is online.
3. If a user modifies configurations simultaneously across multiple devices, the system will merge non-overlapping keys and and resolve conflicts.
4. System will store version history of the configurations so that user can roll-back to previous versions.

## Non Functional Requirements

1. High availability over consistency.
2. Able to handle multiple devices simultaneously.
3. Saved Configuration will be durability.

## Scale

1. Average Config Writes -> 100M DAU * 10 Changes ->  10^4 (Daily Updates)
2. Peek Cofig Writes -> 5 * 10^4
3. Average Sync Reads -> 3 * 10^4 sync QPS
3. Storage -> 3 * 10^8  * 10 KB = 3 TB Storage

## Entities

1. UserDevice
    - deviceId
    - userId
    - deviceType
    - lastSyncedVersion

2. UserConfigurations
    - configurationId
    - userId
    - configurationKey
    - configurationValue
    - version
    - deviceId
    - timestamp

3. ConfigurationSchema
    - schemaId
    - configurationKey
    - dataType
    - configurationValue

## APIs

1. Push Configurations : POST /v1/api/userConfigurations -> body { userId, deviceId, baseVersion, createdAt, [{configurationKey, configurationValue}]}.

2. SignUp : POST /v1/api/configurationSchema -> body{schemaId, [configurationKey, dataType, configurationValue]}.

3. Get Configurations : GET /v1/api/userConfiguraions?{userId}&{version}

4. WebSocket : wss://configuration.gateway.id/userDevice
