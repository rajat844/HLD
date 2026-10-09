# CDN

## Functional Requirements

1. User will be able to download the files such as js files, css files, images and videos.
2. Content owner will be able to create and configure distribution by specifying origin.
3. User will routed to nearest PoP based on the network proximity.
4. CDN will cache data according to cache policies, TTLs and capacity.

## Non Functional Requirements

1. CAP Theorum : System should be highly available.
2. Ultra low latency in delivering the requested content.
3. CDN should be able to large traffic and sudden traffic spikes

## Scale

1. 100M DAU * 10K requests = 10 ^ 7 qps
2. 1M Files * 10 MB = 10TB storage

## APIs

1. Post Distribution details : POST /v1/api/distributions
2. Get distribution details : GET /v1/api/distributions/{distributionId}
3. Download Content: GET /v1/api/contentId

## Entities

1. Content Ownner
    - ownerId

2. Distribution
    - distribution_id
    - ownerId
    - origin_url

3. Cache
    - Key
    - Value
    - TTL
