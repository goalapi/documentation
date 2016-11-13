
# GoalAPI-v1 specification
This is entry point for documentation for GoalAPI.com REST API version 1.0 in human readable format.  
The OpenAPI (swagger) specification [is here](v1/schema/swagger.json)

# GoalAPI Service Overview 

1.  [Current version](#current-version)
1.  [Schema](#schema)
1.  [Authentication](#authentication) 
1.  [Root endpoint](#root-endpoint) 
1.  [HTTP Redirects](#http-redirects) 
1.  [Error responses](#error-responses)
1.  [Pagination](#pagination)
1.  [Working with Matches](v1/docs/Entities/Match.md)

## Current version
By default, all requests receive the **v1** version of the API. We encourage you to explicitly request this version specifying /v1 endpoint after hostname.

## Authentication using API key
There is one way for authentication through GoalAPI-v1: clients must send API key inside `X-AUTH-APIKEY` header. 
The service will send `403 Forbidden` answer, for all requests without valid API key. 

```bash
$ curl -i  'http://api.goalapi.com/v1/tournaments/rus_pl'

HTTP/1.1 403 Forbidden - Request must contain X-AUTH-APIKEY header  
Content-Type: application/json
```
 
In order to work with our service the client must have API key value, regularly we give API keys after registration. Please [contact support](mailto:support@goalapi.com) for more details on registration on our service.

```bash
$ curl -i  'http://api.goalapi.com/v1/' -H "X-AUTH-APIKEY: apikey-value"

HTTP/1.1 200 OK
Content-Type: application/json
```

## Schema
All API access is over HTTP, and accessed from the `http://api.goalapi.com`. Currently **v1** supports only one media type which is _application/json_ and all responses will have `Content-Type: application/json` header. All data is sent and received as JSON.  

```bash
$ curl -i  'http://api.goalapi.com/v1/' -H "X-AUTH-APIKEY: xxx-xxxx-xxx"

HTTP/1.1 200 OK
Content-Type: application/json
X-API-Version: 1

{
    "_links": {
        "tournaments": {
            "href": "/tournaments/"
        }
    },
    "status": "ok",
    "apikey_md5": "e4da3baaaaaaaaaaaaaaaa0674a318d5",
    "expirationTime": {
        "date_time": "2017-08-01T22:49:08+00:00",
        "timestamp": 1501627748
    }
}
```

### _links attribute for each item
We tried to implement some Hypermedia linking in our API. In accordance with [HAL approach](http://blog.stateless.co/post/13296666138/json-linking-with-hal), each entity in GoalAPI responses contains **_links** attribute which contains link to entity itself and also may contain links to related objects. 

```json
    {
        "tournament": {
            "id": "hrv_2h",
            "name": "2 Hnl",
            "_links": {
                "self": {
                    "href": "/tournaments/hrv_2h"
                }
            }
        }
    }
```

### Trailing slashes in URI path
Trailing slash must present in path if client requests the list of items i.e. the server will return the array. If client needs details of one item, he must send request without trailing slash in URI path. 
```
/v1/tournaments/ucl/seasons/ #returns [array of items]
v1/players/bjarnason-aron #returns {one item}
```

If client requests particular item, trailing slash will cause `400 Bad Request - Wrong path` error response. 


### List of items and detailed data about one item
When clients fetch a **list of resources**, the response includes a subset of the attributes for that resource. This is the "summary" representation of the resource. Some data is computationally expensive for the API to provide, also it takes to much traffic bandwidth which may be critical for mobile apps. Due to these reasons, **list of resources** representation provides only basic attributes for each item. 
To get detailed info about particular item clients must request **separate item** by ID. 

**Example.** List of teams taking part in Champions League playoff:

```bash
$ curl -i  'http://api.goalapi.com/v1/tournaments/ucl/seasons/20152016/stages/playoffs/teams/' -H "X-AUTH-APIKEY: xxx-xxxx-xxx"
HTTP/1.1 200 OK
Content-Type: application/json
X-API-Version: 1

[
    {
        "id": "reamad_esp",
        "name": "Real Madrid",
        "_links": {
            "team": {
                "href": "/teams/reamad_esp"
            },
            "self": {
                "href": "/tournaments/ucl/seasons/20152016/stages/playoffs/teams/reamad_esp"
            }
        }
    },
    {
        "id": "atlmad_esp",
        "name": "Atl. Madrid",
        "_links": {
            "team": {
                "href": "/teams/atlmad_esp"
            },
            "self": {
                "href": "/tournaments/ucl/seasons/20152016/stages/playoffs/teams/atlmad_esp"
            }
        }
    },
    {
        "id": "mancit_eng",
        "name": "Manchester City",
        "_links": {
            "team": {
                "href": "/teams/mancit_eng"
            },
            "self": {
                "href": "/tournaments/ucl/seasons/20152016/stages/playoffs/teams/mancit_eng"
            }
        }
    },
    {
        "id": "baymun_deu",
        "name": "Bayern Munich",
        "_links": {
            "team": {
                "href": "/teams/baymun_deu"
            },
            "self": {
                "href": "/tournaments/ucl/seasons/20152016/stages/playoffs/teams/baymun_deu"
            }
        }
    }
]

``` 


**Example.** Detailed info about particular team in this tournament includes info about players:

```bash
$ curl -i  'http://api.goalapi.com/v1/tournaments/ucl/seasons/20152016/stages/playoffs/teams/atlmad_esp' -H "X-AUTH-APIKEY: xxx-xxxx-xxx"
HTTP/1.1 200 OK
Content-Type: application/json
X-API-Version: 1

{
    "id": "atlmad_esp",
    "name": "Atl. Madrid",
    "_links": {
        "team": {
            "href": "/teams/atlmad_esp"
        },
        "self": {
            "href": "/tournaments/ucl/seasons/20152016/stages/playoffs/teams/atlmad_esp"
        }
    },
    "tournament": {
        "id": "ucl",
        "name": "Champions League",
        "_links": {
            "self": {
                "href": "/tournaments/ucl"
            }
        },
        "coverage": {
            "id": "eu",
            "name": "Europe",
            "_links": {
                "self": {
                    "href": "/territories/eu"
                }
            }
        }
    },
    "season": {
        "name": "Champions League 2015/2016",
        "_links": {
            "self": {
                "href": "/tournaments/ucl/seasons/20152016"
            }
        }
    },
    "players": [
        {
            "id": "fernandez-augusto",
            "name": "Fernandez Augusto",
            "_links": {
                "self": {
                    "href": "/players/fernandez-augusto"
                }
            },
            "number": 12
        },
        {
            "id": "luis-filipe",
            "name": "Luis Filipe",
            "_links": {
                "self": {
                    "href": "/players/luis-filipe"
                }
            },
            "number": 3
        },
        {
            "id": "gabi",
            "name": "Gabi",
            "_links": {
                "self": {
                    "href": "/players/gabi"
                }
            },
            "number": 14,
            "captain": true
        }
    ]
}
```

## Root endpoint
Client can issue a GET request to the root endpoint to get information about subscription bound to passed API key. This information information includes such details as subscription status, expiration time and available tournaments: 

```bash
$ curl -i  'http://api.goalapi.com/v1/' -H "X-AUTH-APIKEY: xxx-xxxx-xxx"

HTTP/1.1 200 OK
Content-Type: application/json
X-API-Version: 1

{
    "_links": {
        "tournaments": {
            "href": "/tournaments/"
        }
    },
    "status": "ok",
    "apikey_md5": "e4da3baaaaaaaaaaaaaaaa0674a318d5",
    "expirationTime": {
        "date_time": "2017-08-01T22:49:08+00:00",
        "timestamp": 1501627748
    },
    "allowedTournaments": [
        {
            "id": "arg_ca",
            "name": "Copa Argentina",
            "_links": {
                "self": {
                    "href": "/tournaments/arg_ca"
                }
            }
        }
    ]
}
```

## HTTP Redirects
In most of cases redirects are not necessary in GoalAPI v1. But it uses HTTP redirection where appropriate. Receiving an HTTP redirection is not an error and clients should follow that redirect. Redirect responses will have a `Location` header field which contains the URI of the resource to which the client should repeat the requests.

## Error responses
In case of some unexpected input from clients or possible server failures GoalAPI v1 produces error HTTP-responses. Code of each error response correctly corresponds to reason of failure: 
* **400 Bad Request** means that request URI's path completely wrong or request missed some important data
* **403 Forbidden** means that client not authorized to access certain resource, also it means that client not authenticated at all
* **404 Not Found** means that client tries to access some entity which can not be found by passed ID 
* **500 Server Error** means some problems on server side not related with client request

All error responses have empty body, just header with error explanation

```bash 
curl -i  'http://api.goalapi.com/v1/'

HTTP/1.1 403 Forbidden - Request must contain X-AUTH-APIKEY header
Content-Type: application/json
```

## Pagination
Some of requests designed to return arrays of items and sometimes they would have to return too many items. In order to reduce possible heaviness of such requests we added pagination. Paginated responses contains some additional fields in header: _Link_, _X-Total-Count_, _X-First-Index_, _X-Last-Index_. 

```
$ curl -i  'http://api.goalapi.com/v1/tournaments/eng_pl/seasons/20162017/matches/2/' -H "X-AUTH-APIKEY: xxx-xxxx-xxx"

HTTP/1.1 200 OK
Content-Type: application/json
X-Total-Count: 380
X-First-Index: 128
X-Last-Index: 255
Link: </v1/tournaments/eng_pl/seasons/20162017/matches/1/>; rel="prev",  </v1/tournaments/eng_pl/seasons/20162017/matches/3/>; rel="next"
```

###Link header
The pagination info is included in the Link header. 
```
Link: </v1/tournaments/eng_pl/seasons/20162017/matches/1/>; rel="prev",  </v1/tournaments/eng_pl/seasons/20162017/matches/3/>; rel="next"
```
In some cases pagination is based on page number, but in case of **/v1/updates** pagination is implemented using `lastUpdateTime` parameter, so it is important to follow  Link header values instead of constructing your own URLs


