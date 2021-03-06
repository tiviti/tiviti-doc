# Resources

## Tvitis

### GET /api/v1.0/users/```:user_id```/tviti/```:filter```

Retrieves an array of tvitis sent to or from a particular user, ordered by ```updated_at```, by latest first.

```:filter``` can be one of ```from```, ```to```, ```archived_from```, ```archived_to``` or ```archived```

* ```from``` retrieves all non-archived tvitis sent to this user **from** any other user
* ```to``` retrieves all non-archived tvitis sent from this user **to** any other user
* ```all``` retrieves all non-archived tvitis sent **to or from** this user **to or from** any other user
* ```archived_from``` retrieves all archived tvitis sent to this user **from** any other user
* ```archived_to``` retrieves all archived tvitis sent from this user **to** any other user
* ```archived``` retrieves all archived tvitis sent **to or from** this user
* ```important``` retrieves all tvitis:
  * sent **to** this user with a current status of **1** (new)
  * sent **from** this user with a current status of **4** (can't help)
  * sent **to or from** this user with an overdue deadline and a current status **not** of **5** (complete)

Sample response:

```
{
    "tviti": [
        {
            "id": {
                "$oid": "52fa1cfd3763620002000000"
            },
            "from_id": {
                "$oid": "52f14a26e4b07113cb493147"
            },
            "from_email": "user1@gmail.com",
            "from_first_name": "calvin",
            "from_last_name": "mayer",
            "from_image_profile": "http://domain.com/image_path1.jpg",
            "to_id": {
                "$oid": "52f8b9d33433640002000000"
            },
            "to_email": "user2@mac.com",
            "to_first_name": null,
            "to_last_name": null,
            "to_image_profile": "http://domain.com/image_path2.jpg",
            "created_at": "2014-02-11T12:52:13.932Z",
            "updated_at": "2014-02-15T16:13:12.924Z",
            "name": "abcde",
            "description": "12345",
            "status": 1,
            "deadline": "2014-02-11T00:00:00+00:00",
            "notes": [],
            "status_history": [
                {
                    "_id": {
                        "$oid": "52fa1cfd3763620002010000"
                    },
                    "created_at": "2014-02-11T12:52:13.901Z",
                    "status": 1
                }
            ],
            "deleted": false,
            "archived_to": false,
            "archived_from": false
        }
    ]
} 
```

### GET /api/v1.0/users/```:user1_id```/tviti/```:filter```/```:user2_id```

Retrieves an array of tvitis sent to or from a particular user (user1 above), to or from another user (user2 above), ordered by ```updated_at```, by latest first.

```:filter``` can be one of ```from```, ```to```, ```archived_from``` or ```archived_to```

* ```from``` retrieves all non-archived tvitis sent to user1 **from** user2
* ```to``` retrieves all non-archived tvitis sent from user1 **to** user2
* ```all``` retrieves all non-archived tvitis sent from user1 **to** user2, or to user1 **from** user2
* ```archived_from``` retrieves all archived tvitis sent to user1 **from** user2
* ```archived_to``` retrieves all archived tvitis sent from user1 **to** user2
* ```archived``` retrieves all tvitis sent from user1 to user2 and archived by user2, and all tvitis sent from user2 to user1 and archived by user1

Sample response:

```
{
    "tviti": [
        {
            "id": {
                "$oid": "52fa1cfd3763620002000000"
            },
            "from_id": {
                "$oid": "52f14a26e4b07113cb493147"
            },
            "from_email": "user1@gmail.com",
            "from_first_name": "calvin",
            "from_last_name": "mayer",
            "from_image_profile": "http://domain.com/image_path1.jpg",
            "to_id": {
                "$oid": "52f8b9d33433640002000000"
            },
            "to_email": "user2@mac.com",
            "to_first_name": null,
            "to_last_name": null,
            "to_image_profile": "http://domain.com/image_path1.jpg",
            "created_at": "2014-02-11T12:52:13.932Z",
            "updated_at": "2014-02-15T16:13:12.924Z",
            "name": "abcde",
            "description": "12345",
            "status": 1,
            "deadline": "2014-02-11T00:00:00+00:00",
            "notes": [],
            "status_history": [
                {
                    "_id": {
                        "$oid": "52fa1cfd3763620002010000"
                    },
                    "created_at": "2014-02-11T12:52:13.901Z",
                    "status": 1
                }
            ],
            "deleted": false,
            "archived_to": false,
            "archived_from": false
        }
    ]
} 
```

### GET /api/v1.0/tviti/```:tviti_id```

Retrieves a single tviti by its ```id```.

Sample response:

```
{
    "tviti": {
        "id": {
            "$oid": "52fa1cfd3763620002000000"
        },
        "from_id": {
            "$oid": "52f14a26e4b07113cb493147"
        },
        "from_email": "user1@gmail.com",
        "from_first_name": "calvin",
        "from_last_name": "mayer",
        "to_id": {
            "$oid": "52f8b9d33433640002000000"
        },
        "to_email": "user2@mac.com",
        "to_first_name": null,
        "to_last_name": null,
        "created_at": "2014-02-11T12:52:13.932Z",
        "updated_at": "2014-02-15T16:13:12.924Z",
        "name": "123",
        "description": "445",
        "status": 1,
        "deadline": "2014-02-11T00:00:00+00:00",
        "notes": [],
        "status_history": [
            {
                "_id": {
                    "$oid": "52fa1cfd3763620002010000"
                },
                "created_at": "2014-02-11T12:52:13.901Z",
                "status": 1
            }
        ],
        "deleted": false,
        "archived_to": false,
        "archived_from": false
    }
}
```

### POST /api/v1.0/tviti

Creates a tviti. If ```to_id``` is provided, this will be used. If not, a ```to_email``` must be provided, and the existing user with that email address will be resolved or a new user will be created automatically with a random password.

Sample request:

```
{
    "tviti": {
        "from_id": "52f14a26e4b07113cb493147",
        "to_id": "52f8b9d33433640002000000",
        "name": "12345",
        "description": "abcde",
        "status": 1,
        "deadline": "2014-02-11T00:00:00+00:00",
    }
}
```

Sample response:

```
{
    "tviti": {
        "id": {
            "$oid": "52ff96cc546f623159000000"
        },
        "from_id": {
            "$oid": "52f14a26e4b07113cb493147"
        },
        "from_email": "user1@gmail.com",
        "from_first_name": "calvin",
        "from_last_name": "mayer",
        "to_id": {
            "$oid": "52f8b9d33433640002000000"
        },
        "to_email": "user2@mac.com",
        "to_first_name": null,
        "to_last_name": null,
        "created_at": "2014-02-15T16:33:16.452Z",
        "updated_at": "2014-02-15T16:33:16.457Z",
        "name": "12345",
        "description": "abcde",
        "status": 1,
        "deadline": "2014-02-11T00:00:00+00:00",
        "notes": [],
        "status_history": [
            {
                "_id": {
                    "$oid": "52ff96cc546f623159010000"
                },
                "created_at": "2014-02-15T16:33:16.444Z",
                "status": 1
            }
        ],
        "deleted": false,
        "archived_to": false,
        "archived_from": false
    }
}
```

### POST /api/v1.0/tviti/`:tviti_id`/note

Creates a note. A `by_id` and `text` must be provided inside a `note` attribute. The `by_id` identifies the user creating the note.

When a new note is created, the `chat_viewed_from` or `chat_viewed_to` field on the associated Tviti will be marked `false` according to the user identified by `by_id`. For example, if the `by_id` refers to the 'from' user, `chat_viewed_to` will become false, and vice-versa.

Sample request:

```
{
    "note": {
        "by_id": "52f14a26e4b07113cb493147",
        "text": "Making a note"
    }
}
```

Sample response:

```
{
    "tviti": {
        "id": {
            "$oid": "52ff96cc546f623159000000"
        },
        "from_id": {
            "$oid": "52f14a26e4b07113cb493147"
        },
        "from_email": "user1@gmail.com",
        "from_first_name": "calvin",
        "from_last_name": "mayer",
        "to_id": {
            "$oid": "52f8b9d33433640002000000"
        },
        "to_email": "user2@mac.com",
        "to_first_name": null,
        "to_last_name": null,
        "created_at": "2014-02-15T16:33:16.452Z",
        "updated_at": "2014-02-15T16:33:16.457Z",
        "name": "12345",
        "description": "abcde",
        "status": 1,
        "deadline": "2014-02-11T00:00:00+00:00",
        "notes": [
            {
                "by_id": {
                    "$oid": "52f14a26e4b07113cb493147"
                },
                text: "Making a note"
            }
        ],
        "status_history": [
            {
                "_id": {
                    "$oid": "52ff96cc546f623159010000"
                },
                "created_at": "2014-02-15T16:33:16.444Z",
                "status": 1
            }
        ],
        "deleted": false,
        "archived_to": false,
        "archived_from": false
    }
}
```

### PUT /api/v1.0/tviti/```:tviti_id```

Updates a tviti. In addition to the usual tviti attributes, you can specify ```by_id``` when updating the ```status```. This should be the ```id``` of either the **to** or **from** user. If you don't specify a ```by_id```, the API will assume the **from** user is initiating the update, but in that case it will *not* store the **from** user's ```id``` in the status's ```by_id``` attribute.

Sample request:

```
{
    "tviti": {
        "deadline": "2014-02-13T00:00:00+00:00",
        status: 4,
        by_id: "52f8b9d33433640002000000"
    }
}
```

Sample response:

```
{
    "tviti": {
        "id": {
            "$oid": "52ff96cc546f623159000000"
        },
        "from_id": {
            "$oid": "52f14a26e4b07113cb493147"
        },
        "from_email": "user1@gmail.com",
        "from_first_name": "calvin",
        "from_last_name": "mayer",
        "to_id": {
            "$oid": "52f8b9d33433640002000000"
        },
        "to_email": "user2@mac.com",
        "to_first_name": null,
        "to_last_name": null,
        "created_at": "2014-02-15T16:33:16.452Z",
        "updated_at": "2014-02-15T16:33:16.457Z",
        "name": "12345",
        "description": "abcde",
        "status": 1,
        "deadline": "2014-02-13T00:00:00+00:00",
        "notes": [],
        "status_history": [
            {
                "_id": {
                    "$oid": "52ff96cc546f623159010000"
                },
                "created_at": "2014-02-15T16:33:16.444Z",
                "status": 1
            },
            {
                "_id": {
                    "$oid": "52ff96cc546f623159020000"
                },
                "created_at": "2014-02-15T16:33:16.444Z",
                "status": 4,
                "by_id": {
                  "$oid": "52f8b9d33433640002000000"  
                }
            }
        ],
        "deleted": false,
        "archived_to": false,
        "archived_from": false,
        "chat_viewed_to": false,
        "chat_viewed_from": false
    }
}
```

### POST /api/v1.0/tviti/`:tviti_id`/poke

Pokes the 'to' user. No attributes are permitted, and a successful request will result in an HTTP 201 (Created) response.


### POST /api/v1.0/tviti/`:tviti_id`/thank

Thanks the 'to' user. No attributes are permitted, and a successful request will result in an HTTP 201 (Created) response.


## Users

### GET /api/v1.0/users/```:user_id```

Retrieves a single user.

Sample response:

```
{
    "user": {
        "id": {
            "$oid": "52c7ea633561610002000000"
        },
        "email": "randall.dunn@yahoo.com",
        "first_name": null,
        "last_name": null,
        "google_access_token": "qwertyuiop",
        "image_profile": "12345",
        "device_tokens": ["abcdef0123","0123abcdef"]
    }
}
```

### GET /api/v1.0/users/```:user_id```/stats

Gets tviti stats for a single user. Response is an array of objects, each representing a single user which the specified ```:user_id``` has sent or received tvitis to or from. The array will be ordered by the number of 'open' (i.e. not archived) items between each user and the user referenced by `:user_id`, in descending order.

Sample response:

```
[
    {
        "user_id": {
            "$oid": "52f8b9d33433640002000000"
        },
        "user_email": "elaine-edwards@mac.com",
        "user_first_name": "Elaine",
        "user_last_name": "Edwards",
        "user_image_profile": "http://domain.com/image_path",
        "from_count": 0,
        "archived_from_count": 1,
        "to_count": 2,
        "archived_to_count": 0
    },
    {
        "user_id": {
            "$oid": "52cfdca33838370002010000"
        },
        "user_email": "jon@email.com",
        "user_first_name": "Jon",
        "user_last_name": "Williams",
        "user_image_profile": "http://domain.com/image_path_2",
        "from_count": 1,
        "archived_from_count": 1,
        "to_count": 0,
        "archived_to_count": 0
    }
]
```

### POST /api/v1.0/users

Creates a user. Either a ```password``` **or** a ```google_access_token``` is required.

If a user already exists with the email address, the existing user will be updated. *This needs to be secured.*

Sample request:

```
{
    "user": {
        "email": "user@email.com",
        "first_name": "John",
        "last_name": "Doe",
        "password": "s3cret",
        "password_confirmation": "s3cret",
        "google_access_token": "qwertyuiop",
        "image_profile": "12345",
        "device_tokens": ["abcdef0123","0123abcdef"]
    }
}
```

Sample reponse:

```
{
    "user": {
        "id": {
            "$oid": "52ffc872546f623159020000"
        },
        "email": "user@email.com",
        "first_name": "John",
        "last_name": "Doe",
        "google_access_token": "qwertyuiop",
        "image_profile": "12345",
        "device_tokens": ["abcdef0123","0123abcdef"]
    }
}
```

### PUT /api/v1.0/users/```:user_id```

Updates a user.

Sample request:

```
{
    "user": {
        "email": "new.email@email.com",
    }
}
```

Sample reponse:

```
{
    "user": {
        "id": {
            "$oid": "52ffc872546f623159020000"
        },
        "email": "new.email@email.com",
        "first_name": "John",
        "last_name": "Doe",
        "google_access_token": "qwertyuiop",
        "image_profile": "12345",
        "device_tokens": ["abcdef0123","0123abcdef"]
    }
}
```

### POST /api/v1.0/users/login

Authenticates a user given an email address and password. Successful authentication returns the user as an object; unsuccessful authentication returns a 401 HTTP status.

Sample request:

```
{
    "user": {
        "email": "user@email.com",
        "password": "s3cret"
    }
}
```

Sample reponse:

```
{
    "user": {
        "id": {
            "$oid": "52ffc872546f623159020000"
        },
        "email": "user@email.com",
        "first_name": "John",
        "last_name": "Doe",
        "google_access_token": "qwertyuiop",
        "image_profile": "12345",
        "device_tokens": ["abcdef0123","0123abcdef"]
    }
}
```

### GET /api/v1.0/users/by_email?email=```:email```

Returns the ID of a user given their email address.

Sample response:

```
{
    "user": {
        "id": {
            "$oid": "52f14a26e4b07113cb493147"
        }
    }
}
```

## Device tokens

As well as updating the ```device_tokens``` attribute of the *User* directly, you can add and remove individual device_tokens using this API:


### POST /api/v1.0/users/:user_id/device_tokens

For a specific user, adds a device token if it doesn't already exist.

Sample request:

```
{
    "device_token": "fedcba54321"
}
```

The response will be 201 Created (with no content) regardless of whether the device token has been successfully added, or already existed for that user. 


### DELETE /api/v1.0/users/:user_id/device_tokens/:device_token

For a specific user, removes a device token if it exists.

Sample request: 

```
DELETE /api/v1.0/users/123/device_tokens/fedcba54321
```

No payload is required or permitted.

The response will be 204 No Content regardless of whether the device token has been successfully removed, or didn't exist to start with. 


# Messages configuration

The texts pushed to the notes array and used for push notifications are stored in [/config/locales/en.yml](/config/locales/en.yml).

For **notes**, the format is:

```
en:
  notes:
    status-x:
      by_from: "Message containing the to user's name: %{to_first_name} %{to_last_name"
      by_to: "Message containing the tviti name: %{tviti_name}"
```

where ```x``` is the numerical status code. Leaving out a ```by_from``` or ```by_to``` will mean that the notes array is not updated when the *from* or *to* user updates a tviti to the relevant status, as applicable.

For **push notifications**, the format is:

```
en:
  notifications:
    status-x:
      for_to: "Message containing the to user's name: %{to_first_name} %{to_last_name"
      for_from: "Message containing the tviti name: %{tviti_name}"
```

where ```x``` is the numerical status code. Leaving out a ```for_to``` or ```for_from``` will mean that a push notification is not sent to the *to* or *from* user when the tviti's is updated to the relevant status, as applicable.
