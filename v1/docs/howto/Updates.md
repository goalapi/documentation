# How to process Updates

1. [Overview](#overview)
1. [Updates of Matches](#matches-updates)
1. [Updates pagination](#Pagination)


## Overview 

There is no need to re-get all matches, standings and team squads each time when Client wants to synchronise local data storage with our service.  
If the Client knows when data was updated last time, it's possible to fetch only data which updated since that moment. 
To handle this our service offers [_updates/_ API-call](./../api-calls.md#updates). 
In order to check if any updates happened from some moment, the Client must invoke it with timestamp of that moment passed as _goalapi_notification_timestamp_ query parameter. 

**Example:**
```shell
    $ curl -i 'http://api.goalapi.com/v1/updates/?goalapi_notification_timestamp=1469560782' -H "X-AUTH-APIKEY: xxx-xxxx-xxx"

    HTTP/1.1 200 OK
    Content-Type: application/json
    X-API-Version: 1
    Link: </v1/updates/matches/?goalapi_notification_timestamp=1469560782>; rel="matches",  
          </v1/updates/tournaments/?goalapi_notification_timestamp=1469560782>; rel="tournaments",  
          </v1/updates/seasons/?goalapi_notification_timestamp=1469560782>; rel="seasons",  
          </v1/updates/stages/?goalapi_notification_timestamp=1469560782>; rel="stages",  
          </v1/updates/teams/?goalapi_notification_timestamp=1469560782>; rel="teams",  
          </v1/updates/standings/?goalapi_notification_timestamp=1469560782>; rel="standings"
```

The main part of response of this API-call is _Link_ field of HTTP-header. 
It contains links to API-calls which will return updated data of appropriate type if such updates exists. 
If there are no updated matches link with _rel="matches"_ will not present in header. 

Besides these links in header,  in the body of response _updates/_ API-call returns array of matches updated today (if they exist).  


## How to get Matches Updates

If Client knows that he needs only matches for example, it's possible not call _updates/_, 
but invoke [_updates/matches/_](./../api-calls.md#updates-by-data-types) directly.

**Example:**
```shell
    $ curl -i 'http://api.goalapi.com/v1/updates/matches/?goalapi_notification_timestamp=1469560782' -H "X-AUTH-APIKEY: xxx-xxxx-xxx"
    
    HTTP/1.1 200 OK
    Content-Type: application/json
    X-API-Version: 1
    X-Total-Count: 24513
    Link: </v1/updates/matches/?goalapi_notification_timestamp=1469560782&add=6b6c36e579f42c8af9c039d527258b28>; rel="next"
```
```json 
[
    {
        "id": "01a03752d100f699e2382e0da1ba736d",
        "begin_time": {
            "date_time": "2015-09-19T14:00:00+00:00",
            "timestamp": 1442671200
        },
        "status": {
            "status": "finished",
            "score": [
                1,
                0
            ]
        },
        "tournament": {
            "id": "esp_ll",
            "name": "Primera Division",
            "_links": {
                "self": {
                    "href": "/tournaments/esp_ll"
                }
            },
            "coverage": {
                "id": "esp",
                "name": "Spain",
                "_links": {
                    "self": {
                        "href": "/territories/esp"
                    }
                }
            }
        },
        "teams": [
            {
                "id": "reamad_esp",
                "name": "Real Madrid",
                "_links": {
                    "self": {
                        "href": "/teams/reamad_esp"
                    }
                }
            },
            {
                "id": "gracf_esp",
                "name": "Granada CF",
                "_links": {
                    "self": {
                        "href": "/teams/gracf_esp"
                    }
                }
            }
        ],
        "season": {
            "name": "Primera Division 2015/2016",
            "_links": {
                "self": {
                    "href": "/tournaments/esp_ll/seasons/20152016"
                }
            }
        },
        "stage": {
            "name": "Main",
            "_links": {
                "self": {
                    "href": "/tournaments/esp_ll/seasons/20152016/stages/main"
                }
            }
        },
        "_links": {
            "self": {
                "href": "/tournaments/esp_ll/seasons/20152016/stages/main/matches/01a03752d100f699e2382e0da1ba736d"
            }
        },
        "context": {
            "matchday": "Round 4"
        },
        "last_update_time": {
            "date_time": "2016-07-26T19:19:42+00:00",
            "timestamp": 1469560782
        }
    },
    {
        "id": "01e51ca78912e413dbd3c0ec4aed3bdf",
        "begin_time": {
            "date_time": "2015-12-12T17:15:00+00:00",
            "timestamp": 1449940500
        },
        "status": {
            "status": "finished",
            "score": [
                1,
                2
            ]
        },
        "tournament": {
            "id": "esp_ll",
            "name": "Primera Division",
            "_links": {
                "self": {
                    "href": "/tournaments/esp_ll"
                }
            },
            "coverage": {
                "id": "esp",
                "name": "Spain",
                "_links": {
                    "self": {
                        "href": "/territories/esp"
                    }
                }
            }
        },
        "teams": [
            {
                "id": "lev_esp",
                "name": "Levante",
                "_links": {
                    "self": {
                        "href": "/teams/lev_esp"
                    }
                }
            },
            {
                "id": "gracf_esp",
                "name": "Granada CF",
                "_links": {
                    "self": {
                        "href": "/teams/gracf_esp"
                    }
                }
            }
        ],
        "season": {
            "name": "Primera Division 2015/2016",
            "_links": {
                "self": {
                    "href": "/tournaments/esp_ll/seasons/20152016"
                }
            }
        },
        "stage": {
            "name": "Main",
            "_links": {
                "self": {
                    "href": "/tournaments/esp_ll/seasons/20152016/stages/main"
                }
            }
        },
        "_links": {
            "self": {
                "href": "/tournaments/esp_ll/seasons/20152016/stages/main/matches/01e51ca78912e413dbd3c0ec4aed3bdf"
            }
        },
        "context": {
            "matchday": "Round 15"
        },
        "last_update_time": {
            "date_time": "2016-07-26T19:19:42+00:00",
            "timestamp": 1469560782
        }
    }
]
```
## Pagination
The service returns 128 result at maximum, while number of updates can greater. 
In order to get all matches Client must follow _rel="next"_ link in _Link_ field of response header.   

```
Link: </v1/updates/matches/?goalapi_notification_timestamp=1469560782&add=6b6c36e579f42c8af9c039d527258b28>; rel="next"
```
