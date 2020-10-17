---
title: Audiopedia API Reference

language_tabs:
  # - shell
  # - ruby
  - python
  # - javascript

footer:
  # - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/shamin/greenboard'>Documentation Powered by Greenboard</a>

includes:
  - errors

search: true

attachments:
  - "./logo.png"
---

# Introduction

Welcome to the Audiopedia API! You can use our API to access Audiopedia API endpoints, which can get information on various topics, playlists, and tracks in our database.

Our prefered language binding is in Python. You can view code examples in the dark area to the right!

This API documentation page was created with [Greenboard](https://github.com/shamin/greenboard).

# Authentication

> To authorize, use this code:

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
```

```python
import audiopedia

api = audiopedia.authorize('audiokey')
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
```

> Make sure to replace `audiokey` with your API key.

Audiopedia uses API keys to allow access to the API. You can register a new Audiopedia API key at our [developer portal](http://example.com/developers).

Audiopedia expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: audiokey`

<aside class="notice">
You must replace <code>audiokey</code> with your personal API key.
</aside>


<!-- Tracks -->

# Tracks

## Track Object

### Properties

Parameter | Type | Description
--------- | ------- | -----------
id | AutoField | Unique ID of the track.
title | CharField | Title of the track.
index | IntegerField | The position of the track within a playlist.
audio_url | URLField | URL to the audio file that goes with this track.
transcript | TextField | A string/text transcript that goes along with the audio.
duration | IntegerField | Duration in seconds.
created_at | DateTimeField | When the track was created.
updated_at | DateTimeField | When the track was last updated.
active | BooleanField | Inactivate to temporarily delete track and reactivate to recover.
published | BooleanField | Decide whether this track is ready for users to see.

## Get All Tracks

<!-- ```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import audiopedia

api = audiopedia.authorize('audiokey')
api.tracks.get()
```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let kittens = api.kittens.get();
``` -->

> You fetch all tracks like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all tracks.

### HTTP Request

`GET http://example.com/api/tracks`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Create a Track

<!-- ```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import audiopedia

api = audiopedia.authorize('audiokey')
api.tracks.get(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
``` -->

> You create a track like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint creates a new track.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/tracks/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
Inputs | Examples/descriptions of inputs


## Update a Specific Track

<!-- ```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import audiopedia

api = audiopedia.authorize('audiokey')
api.tracks.delete(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
``` -->

> You update a specific track like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint updates a specific track.

### HTTP Request

`UPDATE http://example.com/tracks/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the track to update


## Delete a Specific Track

<!-- ```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import audiopedia

api = audiopedia.authorize('audiokey')
api.playlists.delete(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
``` -->

> You delete a track like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific track.

### HTTP Request

`DELETE http://example.com/tracks/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the track to delete


<!-- Playlists -->

# Playlists

## Playlist Object

### Properties

Parameter | Type | Description
--------- | ------- | -----------
id | AutoField | Unique ID of the playlist.
title | CharField | The title of the playlist.
index | IntegerField | The position of the playlist within a topic.
audio_url | URLField | URL to the audio directory associated with the playlist.
active | BooleanField | Inactivate to temporarily delete playlist and reactivate to recover.
published | BooleanField | Decide to show or hide the playlist from the users.
tracks | ManytoManyField | A list of all the tracks this playlist contains.

## Get All Playlists

> You fetch all playlists like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all playlists.

### HTTP Request

`GET http://example.com/api/playlists`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Create a Playlist

> You create a playlist like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint creates a new playlist.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/playlists/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the track to retrieve

## Update a Specific Playlist

> You update a specific playlist like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint updates a specific playlist.

### HTTP Request

`DELETE http://example.com/tracks/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the playlist to update


## Delete a Specific Playlist

> You delete a playlist like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific playlist.

### HTTP Request

`DELETE http://example.com/tracks/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the track to delete


<!-- Topics -->

# Topics

## Topic Object

### Properties

Parameter | Type | Description
--------- | ------- | -----------
id | AutoField | Unique ID of the topic.
title | CharField | The name of the topic.
index | IntegerField | The order/position of the topic within the interface.
audio_url | URLField | URL to the audio directory associated with the topic.
active | BooleanField | Inactivate to temporarily delete topic and reactivate to recover.
published | BooleanField | Decide to show or hide the topic from the users.
playlists | ManytoManyField | A list of all the playlists this topic contains.

## Get All Topics

> You can fetch all topics like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all topics.

### HTTP Request

`GET http://example.com/api/topics`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Create a Topic

> You create a topic like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint creates a new topic.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/topics/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the track to retrieve

## Update a Specific Topic

> You update a specific topic like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint updates a specific topic.

### HTTP Request

`DELETE http://example.com/topics/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the topic to update

## Delete a Specific Topic

> You can delete a topic like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific topic.

### HTTP Request

`DELETE http://example.com/topics/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the topic to delete


<!-- Languages -->

# Languages

## Language Object

### Properties

Parameter | Type | Description
--------- | ------- | -----------
id | AutoField | Unique track ID
name | CharField | Name of the language.
audio_url | URLField | URL of audios.
published | BooleanField | Decide whether this language is ready for users to see.

## Get All Languages

> You can fetch all languages like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all languages.

### HTTP Request

`GET http://example.com/api/topics`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Create a Language

> You can create a language like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint creates a new language.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/language/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the language to retrieve


## Update a Specific Language

> You can update a language like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint updates a specific language.

### HTTP Request

`UPDATE http://example.com/language/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the language to update


## Delete a Specific Language

> You can delete a language like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific language.

### HTTP Request

`DELETE http://example.com/language/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the language to delete

