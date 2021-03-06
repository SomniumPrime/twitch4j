+++
title="Streams - Get"
weight = 50
+++

# Get Streams

## Description

Gets information about active streams. Streams are returned sorted by number of current viewers, in descending order. Across multiple pages of results, there may be duplicate or missing streams, as viewers join and leave streams.

The response has a JSON payload with a data field containing an array of stream information elements and a pagination field containing information required to query for more streams.

## Method Definition

```java
@RequestLine("GET /streams?after={after}&before={before}&community_id={community_id}&first={first}&game_id={game_id}&language={language}&user_id={user_id}&user_login={user_login}")
HystrixCommand<StreamList> getStreams(
	@Param("after") String after,
	@Param("before") String before,
	@Param("first") Integer limit,
	@Param("community_id") List<UUID> communityId,
	@Param("game_id") List<Long> gameIds,
	@Param("language") String language,
	@Param("user_id") List<String> userIds,
	@Param("user_login") List<String> userLogins
);
```

*Required Parameters*

None

*Optional Parameters*

| Name          | Type      | Description  |
| ------------- |:---------:| -----------------:|
| after | string | Cursor for forward pagination: tells the server where to start fetching the next set of results, in a multi-page response. The cursor value specified here is from the pagination response field of a prior query. |
| before | string | Cursor for backward pagination: tells the server where to start fetching the next set of results, in a multi-page response. The cursor value specified here is from the pagination response field of a prior query. |
| limit | string | Maximum number of objects to return. Maximum: 100. Default: 20. |
| community_id | string | Returns streams in a specified community ID. You can specify up to 100 IDs. |
| game_id | string |  	Returns streams broadcasting a specified game ID. You can specify up to 100 IDs. |
| language | string | Stream language. You can specify up to 100 languages. |
| user_id | string | Returns streams broadcast by one or more specified user IDs. You can specify up to 100 IDs. |
| user_login | string | Returns streams broadcast by one or more specified user login names. You can specify up to 100 names. |


## Code-Snippets

### get the top 5 streams
```java
StreamList resultList = twitchClient.getHelix().getStreams("", "", null, 5, null, null, null, null).execute();
resultList.getStreams().forEach(stream -> {
    System.out.println("ID: " + stream.getId() + " - Title: " + stream.getTitle());
});
```
