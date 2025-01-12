---
title: Group Management
excerpt: >-
  Manage your WhatsApp groups and their admins. Learn how to add or remove
  members of the different groups.
---
A collection of endpoints used to manage groups that are linked to a specific bot.
  - [Creating a new group](doc:whatsapp-group-management#section-create-group-endpoint)
  - [Listing all groups associated with your bot](doc:whatsapp-group-management#section-list-groups-endpoint)
  - [List all information for a specific group](doc:whatsapp-group-management#section-list-group-information-endpoint)
  - [Updating a groups subject](doc:whatsapp-group-management#section-update-group-subject-endpoint)
  - [Updating a groups icon](doc:whatsapp-group-management#section-update-group-icon-endpoint)
  - [Leaving a group created by your bot](doc:whatsapp-group-management#section-leave-group-endpoint)
  - [Remove group members from a specific group](doc:whatsapp-group-management#section-remove-members-endpoint)
  - [Add admins to a specific group](doc:whatsapp-group-management#section-add-admins-endpoint)
  - [Remove admins from a specific group](doc:whatsapp-group-management#section-remove-admins-endpoint)
  - [Get an invite link to a specific group](doc:whatsapp-group-management#section-get-invite-link-endpoint)
  - [Remove an active invite link from a specific group](doc:whatsapp-group-management#section-remove-invite-link-endpoint)

## Create group endpoint

`POST whatsapp/v1/{bot-id}/groups`

JSON object parameters:

| Name    | Description                      | JSON Type    | Default    | Constraints           | Required |
| ------- | :------------------------------: | :----------: | :--------: | :-------------------: | :------: |
| subject | Group subject                    | String       | N/A        | None                  | Yes      |

### Create group sample

```json
{
  "subject": "Sinch WhatsApp Team Group"
}
```

#### Responses

`200 OK`

The response body is a JSON object with the following parameters:

|Name          | Description                    | JSON Type     |
|--------------|--------------------------------|---------------|
|group_id      | Group id of just created group | String        |

**Sample**

```json
{
  "group_id": "group:447506616260-1565342732"
}
```

`400 Bad Request`

There was an error with your request. The body is a JSON object described in the [introduction](doc:whatsapp-introduction#section-http-errors).

`401 Unauthorized`

There was an authentication error with your request. Either you're using incorrect credentials or you're attempting to authenticate
in a region where your bot does not reside. The body is a JSON object described in the [introduction](doc:whatsapp-introduction#section-http-errors).

## List groups endpoint

`GET whatsapp/v1/{bot-id}/groups`

#### Responses

`200 OK`

The response body is a JSON object with the following parameters:

|Name          | Description                       | JSON Type     |
|--------------|-----------------------------------|---------------|
|groups        | Array of string group identifiers | String array  |

**Sample**

```json
{
  "groups": [
    "group:447506616260-1565342732"
  ]
}
```

`400 Bad Request`

There was an error with your request. The body is a JSON object described in the [introduction](doc:whatsapp-introduction#section-http-errors).

`401 Unauthorized`

There was an authentication error with your request. Either you're using incorrect credentials or you're attempting to authenticate
in a region where your bot does not reside. The body is a JSON object described in the [introduction](doc:whatsapp-introduction#section-http-errors).

## List group information endpoint

`GET whatsapp/v1/{bot-id}/groups/{group-id}`

#### Responses

`200 OK`

The response body is a JSON object with the following parameters:

| Name          | Description                               | JSON Type    |
| ------------- | ----------------------------------------- | ------------ |
| admins        | Array of the WhatsApp identity of all admins | String array |
| creation_time | ISO-8601 creation datetime of the group   | String       |
| creator       | WhatsApp identity of the creator of the group        | String       |
| members       | Array of WhatsApp identities for members in the group | String array |
| subject       | Subject of the group                      | String       |

**Sample**

```json
{
    "admins": [
        "1805550000"
    ],
    "creator": "1805550000",
    "members": [
        "1805550000",
        "46732001122"
    ],
    "subject": "Sinch Team WhatsApp Group",
    "creation_time": "2019-09-23T07:56:22.000Z"
}
```

`400 Bad Request`

There was an error with your request. The body is a JSON object described in the [introduction](doc:whatsapp-introduction#section-http-errors).

`401 Unauthorized`

There was an authentication error with your request. Either you're using incorrect credentials or you're attempting to authenticate
in a region where your bot does not reside. The body is a JSON object described in the [introduction](doc:whatsapp-introduction#section-http-errors).

## Update group subject endpoint

`PATCH whatsapp/v1/{bot-id}/groups/{group-id}`

JSON object parameters:

| Name    | Description                      | JSON Type    | Default    | Constraints           | Required |
| ------- | -------------------------------- | ------------ | ---------- | --------------------- | :------: |
| subject | Group subject                    | String       | N/A        | None                  | Yes      |

### Update group subject sample

```json
{
  "subject": "Updated Sinch WhatsApp Team Group"
}
```

#### Responses

`200 OK`

Empty response body

`400 Bad Request`

There was an error with your request. The body is a JSON object described in the [introduction](doc:whatsapp-introduction#section-http-errors).

`401 Unauthorized`

There was an authentication error with your request. Either you're using incorrect credentials or you're attempting to authenticate
in a region where your bot does not reside. The body is a JSON object described in the [introduction](doc:whatsapp-introduction#section-http-errors).

## Update group icon endpoint

`POST whatsapp/v1/{bot-id}/groups/{group-id}/icon`

JSON object parameters:

| Name    | Description                      | JSON Type    | Default    | Constraints           | Required |
| ------- | -------------------------------- | ------------ | ---------- | --------------------- | :------: |
| url     | Public url of group icon         | String       | N/A        | Valid URL, jpeg/png   | Yes      |


### Update group icon sample

```json
{
  "url": "https://www.example.com/new_icon.jpg"
}
```

#### Responses

`200 OK`

Empty response body

`400 Bad Request`

There was an error with your request. The body is a JSON object described in the [introduction](doc:whatsapp-introduction#section-http-errors).

`401 Unauthorized`

There was an authentication error with your request. Either you're using incorrect credentials or you're attempting to authenticate
in a region where your bot does not reside. The body is a JSON object described in the [introduction](doc:whatsapp-introduction#section-http-errors).

## Leave group endpoint

`DELETE whatsapp/v1/{bot-id}/groups/{group-id}`

#### Responses

`200 OK`

Empty response body

`400 Bad Request`

There was an error with your request. The body is a JSON object described in the [introduction](doc:whatsapp-introduction#section-http-errors).

`401 Unauthorized`

There was an authentication error with your request. Either you're using incorrect credentials or you're attempting to authenticate
in a region where your bot does not reside. The body is a JSON object described in the [introduction](doc:whatsapp-introduction#section-http-errors).

## Remove members endpoint

`DELETE whatsapp/v1/{bot-id}/groups/{group-id}/member`

JSON object parameters:

| Name    | Description                      | JSON Type    | Default    | Constraints           | Required |
| ------- | -------------------------------- | ------------ | ---------- | --------------------- | :------: |
| numbers | List of international phone numbers | String array | N/A        | 1 to 20 elements      | Yes      |

### Remove members sample

```json
{
  "numbers": [
    "46732001122",
    "46732002244"
  ]
}
```

#### Responses

`200 OK`

Empty response body

`400 Bad Request`

There was an error with your request. The body is a JSON object described in the [introduction](doc:whatsapp-introduction#section-http-errors).

`401 Unauthorized`

There was an authentication error with your request. Either you're using incorrect credentials or you're attempting to authenticate
in a region where your bot does not reside. The body is a JSON object described in the [introduction](doc:whatsapp-introduction#section-http-errors).

## Add admins endpoint

`POST whatsapp/v1/{bot-id}/groups/{group-id}/admin`

JSON object parameters:

| Name    | Description                      | JSON Type    | Default    | Constraints           | Required |
| ------- | -------------------------------- | ------------ | ---------- | --------------------- | :------: |
| numbers | List of international phone numbers | String array | N/A        | 1 to 20 elements      | Yes      |

### Add admins sample

```json
{
  "numbers": [
    "46732001122",
    "46732002244"
  ]
}
```

#### Responses

`200 OK`

Empty response body

`400 Bad Request`

There was an error with your request. The body is a JSON object described in the [introduction](doc:whatsapp-introduction#section-http-errors).

`401 Unauthorized`

There was an authentication error with your request. Either you're using incorrect credentials or you're attempting to authenticate
in a region where your bot does not reside. The body is a JSON object described in the [introduction](doc:whatsapp-introduction#section-http-errors).

## Remove admins endpoint

`DELETE whatsapp/v1/{bot-id}/groups/{group-id}/admin`

JSON object parameters:

| Name    | Description                      | JSON Type    | Default    | Constraints           | Required |
| ------- | -------------------------------- | ------------ | ---------- | --------------------- | :------: |
| numbers | List of international phone numbers | String array | N/A        | 1 to 20 elements      | Yes      |

### Remove admins sample

```json
{
  "numbers": [
    "46732001122",
    "46732002244"
  ]
}
```

#### Responses

`200 OK`

Empty response body

`400 Bad Request`

There was an error with your request. The body is a JSON object described in the [introduction](doc:whatsapp-introduction#section-http-errors).

`401 Unauthorized`

There was an authentication error with your request. Either you're using incorrect credentials or you're attempting to authenticate
in a region where your bot does not reside. The body is a JSON object described in the [introduction](doc:whatsapp-introduction#section-http-errors).

## Get invite link endpoint

`GET whatsapp/v1/{bot-id}/groups/{group-id}/invite`

#### Responses

`200 OK`

The response body is a JSON object with the following parameters:

| Name          | Description                               | JSON Type    |
| ------------- | ----------------------------------------- | ------------ |
| invite_link   | Public url of link. Any WhatsApp user who clicks this link will join the group that this link relates to | String array |

**Sample**

```json
{
    "invite_link": "https://chat.whatsapp.com/<invite-link>"
}
```

`400 Bad Request`

There was an error with your request. The body is a JSON object described in the [introduction](doc:whatsapp-introduction#section-http-errors).

`401 Unauthorized`

There was an authentication error with your request. Either you're using incorrect credentials or you're attempting to authenticate
in a region where your bot does not reside. The body is a JSON object described in the [introduction](doc:whatsapp-introduction#section-http-errors).

## Remove invite link endpoint

`DELETE whatsapp/v1/{bot-id}/groups/{group-id}/invite`

#### Responses

`200 OK`

Empty response body

`400 Bad Request`

There was an error with your request. The body is a JSON object described in the [introduction](doc:whatsapp-introduction#section-http-errors).

`401 Unauthorized`

There was an authentication error with your request. Either you're using incorrect credentials or you're attempting to authenticate
in a region where your bot does not reside. The body is a JSON object described in the [introduction](doc:whatsapp-introduction#section-http-errors).
