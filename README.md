# Resources

## Tvitis

### GET /api/v1.0/users/```:user_id```/tviti/```:filter```

Retrieves a list of tvitis sent to or from a particular user, ordered by ```updated_at```, by latest first.

```:filter``` can be one of ```from```, ```to```, ```archived_from``` or ```archived_to```

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
            "to_id": {
                "$oid": "52f8b9d33433640002000000"
            },
            "to_email": "user2@mac.com",
            "to_first_name": null,
            "to_last_name": null,
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

Retrieves a single tviti.

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

### PUT /api/v1.0/tviti/```:tviti_id```

Updates a tviti. 

Sample request:

```
{
    "tviti": {
        "deadline": "2014-02-13T00:00:00+00:00",
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
            }
        ],
        "deleted": false,
        "archived_to": false,
        "archived_from": false
    }
}
```

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

Gets tviti stats for a single user. Response is an array of objects, each representing a single user which the specified ```:user_id``` has sent or received tvitis to or from.

Sample response:

```
[
    {
        "user_id": {
            "$oid": "52f8b9d33433640002000000"
        },
        "user_email": "elaine-edwards@mac.com",
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
        "from_count": 1,
        "archived_from_count": 1,
        "to_count": 0,
        "archived_to_count": 0
    }
]
```

### POST /api/v1.0/users

Creates a user.

Sample request:

```
{
    "user": {
        "email": "user@email.com",
        "first_name": "John",
        "last_name": "Doe",
        "password": "s3cret",
        "password_confirmation": "s3cret"
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

