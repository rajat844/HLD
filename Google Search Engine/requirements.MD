# Google Search Engine

## Functional Requirements

1. User can enter the text query and receive web results.
2. Show query suggestions as the user types.
3. Engine shall return ranked results containing Title, URL and Snippet.
4. Search engine shall continously crawl the webpagest to find the relevant results.
5. User should be able to apply filters to the search.
6. Search history should be maintained

## Non Functional Requirements

1. Search should be highly available.
2. Search results should be shown in less than 1s.
3. Search result should be highly relevant.
4. Search result shall support pagination.
5. Suggestions shall be based on popular and personalized queries.
6. Discover new pages and periodically recrawl existing pages for updates.

## Scale

1. Average Traffic: 5B users * 200 queries a day = 10 ^ 4 qps
2. Peek Traffic: 3 * 10 ^ 4 qps
3. Storage : 30B pages * 1MB = 30PB

## APIs

1. Search : GET /v1/search?q={query}&yype:{searchType}&location{location}&order{order}&page{page}
2. Suggestions : GET /v1/suggestions?q={query}

## Entities

1. User
2. History
3. Suggestions
4. Webpage
5. Document

## Data Model

1. User
    - userId
    - location

2. History
    - queryId
    - userId
    - query
    - timestamp

3. Webpage
    - pageId
    - url
    - title
    - content
    - lastModified

4. Document
    - term
    - pageId
    - score


