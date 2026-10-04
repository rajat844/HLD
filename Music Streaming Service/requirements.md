## HLD
### Functional Requirements
- Artist can upload the songs
- User can access, stream and download song library.
- User can search the song, artist, album.
- User can create playlists.
- Song recommendation system will also be there as per user listening hisory.
- Downloaded songs can be played offline.
- Streaming supports adaptive audio quality
- Save one year of users listening history

### Non Functional Requirements
- 1 PB -> Storage
- 50k -> qps for searching songs
- 20k -> qps for playing songs
- 1Tbps for stream speed
- Recommendation system implementation will be out of scope as it is covered in AI interviews.

### Entities 
- User
    - userId (Primary Key)
    - name
    - email
- SongAnalytics
    - eventId
    - songId (SongAnalytic - Song N:1)
    - userId (User - SongAnalytics 1 : N)
    - sessionId
    - eventTimeStamp
    - startTimeStamp
    - endTimeStamp
- Song
    - songId (Primary Key)
    - albumId (Song - Album N:1)
    - title
    - duration
- SongMediaAsset
    - assetId
    - songId
    - qualityTier
    - bitrate
    - format
    - storageURL
- Artist
    - artistId (Primary Key)
    - name
- Playlist
    - playlistId (Primary Key)
    - createdBy (Playlist - User N:1)
    - name
    - description
    - isPublic
- PlaylistSong
    - playlistItemId
    - playlistId(Primary Key, Foriegn Key)
    - songId (Primary Key, Foreign Key)
    - position 
    - addedAt
- Album 
    - albumId (Primary Key)
    - titleId
    - releaseDate


### API Design

- GET /search?q={query}&type={type}&limit{limit}&offset{offset} -> 200 OK
- GET /song={songId}/playback-session
- POST /playlist body {
    "userId": "$userId",
    "name": "$name$,
    "description": "$description",
    "isPublic": "$isPublic"
} 
- DELETE /playlists={playlistId}/items={itemsId}
- PATCH /playlist={playlistId}/items={itemsId}
- POST /songAnalystics/events



