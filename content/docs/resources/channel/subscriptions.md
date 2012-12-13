# Channel Subscription

* TOC
{:toc}

## Get current user's subscribed channels

Retrieve an "inbox" of the channels the user is currently subscribed to. This stream is ordered like an inbox with the stream containing the most recent post first.

This endpoint responds to [pagination parameters](/appdotnet/api-spec/blob/master/responses.md#pagination-metadata"). Remember that the ```min_id```/```max_id``` do not have to correspond to the ids in the ```data``` list.

<%= migration_warning ['response_envelope'] %>

### URL
> https://alpha-api.app.net/stream/0/channels

### Parameters

None.

### Example

> GET https://alpha-api.app.net/stream/0/channels

~~~ js
{
    "data": [
        {
            "has_unread": true,
            "id": "1",
            "owner": {
                ...
            },
            "readers": {
                "any_user": false,
                "immutable": true,
                "public": false,
                "user_ids": [],
                "you": true
            },
            "type": "net.app.core.pm",
            "writers": {
                "any_user": false,
                "immutable": true,
                "public": false,
                "user_ids": [
                    "1",
                ],
                "you": true
            },
            "you_can_edit": false,
            "you_subscribed": true
        },
        ...
    ],
    "meta": {
        "code": 200,
        "max_id": 146,
        "min_id": 123,
        "more": true
    }
}
~~~

## Subscribe to a Channel

Subscribe to a Channel. This adds it to your [Channel stream](#get-current-users-subscribed-channels).

<%= migration_warning ['response_envelope'] %>

### URL
> https://alpha-api.app.net/stream/0/channels/[channel_id]/subscribe

### Data

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Required?</th>
            <th>Type</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>channel_id</code></td>
            <td>Required</td>
            <td>int</td>
            <td>The id of the Channel to update</td>
        </tr>
    </tbody>
</table>

### Example

> POST https://alpha-api.app.net/stream/0/channels/[channel_id]/subscribe

~~~ js
{
    "data": {
        "has_unread": false,
        "id": "1",
        "owner": {
            ...
        },
        "readers": {
            "any_user": false,
            "immutable": false,
            "public": false,
            "user_ids": [],
            "you": true
        },
        "type": "com.example",
        "writers": {
            "any_user": false,
            "immutable": false,
            "public": false,
            "user_ids": [
                "1"
            ],
            "you": true
        },
        "you_can_edit": true,
        "you_subscribed": true
    },
    "meta": {
        "code": 200
    }
}
~~~

## Unsubscribe from a Channel

Unsubscribe from a Channel. This removes it from your [Channel stream](#get-current-users-subscribed-channels).

<%= migration_warning ['response_envelope'] %>

### URL
> https://alpha-api.app.net/stream/0/channels/[channel_id]/subscribe

### Data

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Required?</th>
            <th>Type</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>channel_id</code></td>
            <td>Required</td>
            <td>int</td>
            <td>The id of the Channel to update</td>
        </tr>
    </tbody>
</table>

### Example

> DELETE https://alpha-api.app.net/stream/0/channels/[channel_id]/subscribe

~~~ js
{
    "data": {
        "has_unread": false,
        "id": "1",
        "owner": {
            ...
        },
        "readers": {
            "any_user": false,
            "immutable": false,
            "public": false,
            "user_ids": [],
            "you": true
        },
        "type": "com.example",
        "writers": {
            "any_user": false,
            "immutable": false,
            "public": false,
            "user_ids": [
                "1"
            ],
            "you": true
        },
        "you_can_edit": true,
        "you_subscribed": false
    },
    "meta": {
        "code": 200
    }
}
~~~

## Retrieve users subscribed to a Channel

Retrieve the users who are subscribed to a Channel.

This endpoint responds to [pagination parameters](/appdotnet/api-spec/blob/master/responses.md#pagination-metadata"). Remember that the ```min_id```/```max_id``` do not have to correspond to the ids in the ```data``` list.

<%= migration_warning ['response_envelope'] %>

### URL
> https://alpha-api.app.net/stream/0/channels/[channel_id]/subscribers

### Parameters

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Required?</th>
            <th>Type</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>channel_id</code></td>
            <td>Required</td>
            <td>int</td>
            <td>The id of the Channel to update</td>
        </tr>
    </tbody>
</table>

### Example

> GET https://alpha-api.app.net/stream/0/channels/1/subscribers

~~~ js
{
    "data": [
        {
            "id": "1", // note this is a string
            "username": "mthurman",
            "name": "Mark Thurman",
            "description": {
               "text": "Hi, I'm Mark Thurman and I'm teaching you about the @appdotnet Stream #API.",
               "html": "Hi, I'm Mark Thurman and I'm <a href=\"https://github.com/appdotnet/api_spec\" rel=\"nofollow\">teaching you</a> about the <span itemprop=\"mention\" data-mention-name=\"appdotnet\" data-mention-id=\"3\">@appdotnet</span> Stream #<span itemprop=\"hashtag\" data-hashtag-name=\"api\">API</span>.",
               "entities": {
                   "mentions": [{
                       "name": "appdotnet",
                       "id": "3",
                       "pos": 52,
                       "len": 10
                   }],
                   "hashtags": [{
                       "name": "api",
                       "pos": 70,
                       "len": 4
                   }],
                   "links": [{
                       "text": "teaching you",
                       "url": "https://github.com/appdotnet/api-spec",
                       "pos": 29,
                       "len": 12
                   }]
                }
            },
            "timezone": "US/Pacific",
            "locale": "en_US",
            "avatar_image": {
                "height": 512,
                "width": 512,
                "url": "https://example.com/avatar_image.jpg"
            },
            "cover_image": {
                "height": 118,
                "width": 320,
                "url": "https://example.com/cover_image.jpg"
            },
            "type": "human",
            "created_at": "2012-07-16T17:23:34Z",
            "counts": {
                "following": 100,
                "followers": 200,
                "posts": 24,
                "stars": 76
            },
            "follows_you": false,
            "you_follow": true,
            "you_muted": false,
        },
        ...
    ],
    "meta": {
        "code": 200,
        "max_id": 82,
        "min_id": 54,
        "more": true
    }
}
~~~

## Retrieve user ids subscribed to a Channel

Retrieve all the user ids who are subscribed to a Channel.

<%= migration_warning ['response_envelope'] %>

### URL
> https://alpha-api.app.net/stream/0/channels/[channel_id]/subscribers/ids

### Parameters

<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Required?</th>
            <th>Type</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>channel_id</code></td>
            <td>Required</td>
            <td>int</td>
            <td>The id of the Channel to update</td>
        </tr>
    </tbody>
</table>

### Example

> GET https://alpha-api.app.net/stream/0/channels/1/subscribers

~~~ js
{
    "data": [
        "1",
        ...
    ],
    "meta": {
        "code": 200,
    }
}
~~~