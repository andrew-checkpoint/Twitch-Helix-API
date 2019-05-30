# Additions

Forked changed:

1. clips.getClips()
1. games.getTopGames()
1. pagination for videos.getVideos()
1. added ratelimit details into response object

# Twitch-Helix-API

[![npm Stats](https://nodei.co/npm/twitch-helix-api.png?downloads=true&downloadRank=true&stars=true)](https://www.npmjs.com/package/twitch-helix-api)

## About

Twitch-Helix-API is a NPM library designed to make use of the Twitch Helix API version easier. It currently covers the following endpoints:

- Get Access Token (Kraken Endpoint)
- Get Games
- Get Streams
- Get Streams Metadata
- Get Users
- Get User Follows
- Update User
- Get Videos

Webhooks are not supported in this library unforuntately. 

## Issues

If you have a suggestion or have discovered a bug relating to this library, please create an issue [here](https://github.com/Glyciant/Twitch-Helix-API/issues). Ensure you are as descriptive as possible.

## Contributions

You may contribute to this library if you wish to. Please create a pull request to do so.

## Installation

Install with NPM:

`npm install --save twitch-helix-api`

## Documentation & Usage

Begin by importing the library and setting a Client ID. Example:

```
var api = require("twitch-helix-api");

api.clientID = "XXXXXXXXXXXXXXXXXXXXX";
```

### Requests

#### Authentication

##### Get Access Token

Usage:

```
api.authentication.getAccessToken({ ... }).then(function(data) {
    ...
});
```

This request requires you to have already received an authorization code from Twitch. Refer to the Twitch documentation if you do not know how to do this.

You must send all of these parameters in the object:

|**Name**|**Type**|**Description**|
|--- |--- |--- |
|`client_id`|string|Your client ID.|
|`client_secret`|string|Your client secret.|
|`redirect_uri`|string|Your registered redirect URI. This must exactly match the redirect URI registered.|
|`code`|string|Your authorization code sent by Twitch.|

You may send these optional parameters in the object:

|**Name**|**Type**|**Description**|
|--- |--- |--- |
|`state`|string|Your unique token, generated by your application. This is an OAuth 2.0 opaque value, used to avoid CSRF attacks. This value is echoed back in the response.|

##### Check Token

```
api.authentication.checkToken({ ... }).then(function(data) {
    ...
});
```

This request requires you to have an access token.

|**Name**|**Type**|**Description**|
|--- |--- |--- |
|`token`|string|Your access token from Twitch.|

#### Games

##### Get Games

Usage:

```
api.games.getGames({ ... }).then(function(data) {
    ...
});
```

This request accepts no authentication.

This request requires no parameters.

You may send these optional parameters in the object:

|**Name**|**Type**|**Description**|
|--- |--- |--- |
|`id`|string|Game ID. At most 100 id values can be specified.|
|`name`|string|Game name. The name must be an exact match. For instance, "Pokemon" will not return a list of Pokemon games; instead, query the specific Pokemon game(s) in which you are interested. At most 100 name values can be specified.|

#### Streams

##### Get Streams

Usage: 

```
api.streams.getStreams({ ... }).then(function(data) {
    ...
});
```

This request accepts no authentication.

This request requires no parameters.

You may send these optional parameters in the object:

|**Name**|**Type**|**Description**|
|--- |--- |--- |
|`after`|string|Cursor for forward pagination: tells the server where to start fetching the next set of results, in a multi-page response.|
|`before`|string|Cursor for backward pagination: tells the server where to start fetching the next set of results, in a multi-page response.|
|`community_id`|string|Returns streams in a specified community ID. You can specify up to 100 IDs.|
|`first`|integer|Maximum number of objects to return. Maximum: 100. Default: 20.|
|`game_id`|string|Returns streams broadcasting a specified game ID. You can specify up to 100 IDs.|
|`language`|string|Stream language. You can specify up to 100 languages.|
|`type`|string|Stream type: "all", "live", "vodcast". Default: "all".|
|`user_id`|string|Returns streams broadcast by one or more specified user IDs. You can specify up to 100 IDs.|
|`user_login`|string|Returns streams broadcast by one or more specified user login names. You can specify up to 100 names.|

##### Get Streams Metadata

Usage: 

```
api.streams.getStreamsMetadata({ ... }).then(function(data) {
    ...    ...
});
```

This request accepts no authentication.

This request requires no parameters.

You may send these optional parameters in the object:

|**Name**|**Type**|**Description**|
|--- |--- |--- |
|`after`|string|Cursor for forward pagination: tells the server where to start fetching the next set of results, in a multi-page response.|
|`before`|string|Cursor for backward pagination: tells the server where to start fetching the next set of results, in a multi-page response.|
|`community_id`|string|Returns streams in a specified community ID. You can specify up to 100 IDs.|
|`first`|integer|Maximum number of objects to return. Maximum: 100. Default: 20.|
|`game_id`|string|Returns streams broadcasting a specified game ID. You can specify up to 100 IDs.|
|`language`|string|Stream language. You can specify up to 100 languages.|
|`type`|string|Stream type: "all", "live", "vodcast". Default: "all".|
|`user_id`|string|Returns streams broadcast by one or more specified user IDs. You can specify up to 100 IDs.|
|`user_login`|string|Returns streams broadcast by one or more specified user login names. You can specify up to 100 names.|

#### Users

##### Get Users

Usage:

```
api.users.getUsers({ ... }).then(function(data) {
    ...
});
```

This request requires no authentication, but accepts the `user:read:email` to send en email address.

You must send one or more of these parameters in the object:

|**Name**|**Type**|**Description**|
|--- |--- |--- |
|`ìd`|string|User ID. Multiple user IDs can be specified. Limit: 100.|
|`login`|string|User login name. Multiple login names can be specified. Limit: 100.|

This request has no optional parameters.

##### Get Users Follows

Usage:

```
api.users.getUsersFollows({ ... }).then(function(data) {
    ...
});
```

This request accepts no authentication.

You must send one or more of these parameters in the object:

|**Name**|**Type**|**Description**|
|--- |--- |--- |
|`from_id`|string|User ID. The request returns information about users who are being followed by the `from_id` user.|
|`to_id`|string|User ID. The request returns information about users who are following the `to_id` user.|

You may send these optional parameters in the object:

|**Name**|**Type**|**Description**|
|--- |--- |--- |
|`after`|string|Cursor for forward pagination: tells the server where to start fetching the next set of results, in a multi-page response.|
|`before`|string|Cursor for backward pagination: tells the server where to start fetching the next set of results, in a multi-page response.|
|`first`|integer|Maximum number of objects to return. Maximum: 100. Default: 20.|

##### Update Users

Usage:

```
api.users.updateUsers({ ... }).then(function(data) {
    ...
});
```

This request requires authentication. The `user:edit` scope is required.

You must send one or more of these parameters in the object:

|**Name**|**Type**|**Description**|
|--- |--- |--- |
|`description`|string|New user description: used to set the new description for the user.|

This request has no optional parameters.

#### Videos

#### Get Videos

Usage:

```
api.videos.getVideos({ ... }).then(function(data) {
    ...
});
```

This request accepts no authentication.

You must send one or more of these parameters in the object:

|**Name**|**Type**|**Description**|
|--- |--- |--- |
|`id`|string|ID of the video being queried. Limit: 100. If this is specified, you cannot use any of the optional query string parameters below.|
|`user_id`|string|ID of the user who owns the video. Limit 1.|
|`game_id`|string|ID of the game the video is of. Limit 1.|

You may send these optional parameters in the object:

|**Name**|**Type**|**Description**|
|--- |--- |--- |
|`after`|string|Cursor for forward pagination: tells the server where to start fetching the next set of results, in a multi-page response.|
|`before`|string|Cursor for backward pagination: tells the server where to start fetching the next set of results, in a multi-page response.|
|`first`|string|Number of values to be returned when getting videos by user or game ID. Limit: 100. Default: 20.|
|`language`|string|Language of the video being queried. Limit: 1.|
|`period`|string|Period during which the video was created. Valid values: "all", "day", "month", and "week". Default: "all".|
|`sort`|string|Sort order of the videos. Valid values: "time", "trending", and "views". Default: "time".|
|`type`|string|Type of video. Valid values: "all", "upload", "archive", and "highlight". Default: "all".|

### Responses

All requests made will return a custom payload object containing the data you requested along with other useful information.

Example successful response:

```
{ 
    code: 200,
    status: "success",
    message: "OK",
    response: ...
}
```

Example error response:

```
{
    code: 400,
    status: "bad_request",
    message: ...,
    response: null
}
```

The `message` field will describe the exact error you have made.

The `response` field will contain whatever data Twitch sends as a response to your request.