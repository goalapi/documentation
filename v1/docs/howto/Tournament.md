# Tournaments
This describes API-calls to fetch data about Tournaments current Subscription has access to  

1. [List all Tournaments available for current API-key](#list-all-tournaments-available-for-current-api-key)
1. [Get Tournament by ID](#get-tournament-by-id)
1. [Tournament properties explained](#tournament-properties-explained)
1. [Get Matches and other data from Tournament](#get-matches-and-other-data-from-tournament)

## List all Tournaments available for current API-key

```
    GET /v1/tournaments/
```

This API-call returns array of Tournament items available for API-key   

**Example:**
```
$ curl -i 'http://api.goalapi.com/v1/tournaments/' -H "X-AUTH-APIKEY: xxx-xxxx-xxx"

HTTP/1.1 200 OK
Content-Type: application/json
X-API-Version: 1
```
```json
[
    {
        "id": "aut_oc",
        "name": "Ofb Cup",
        "_links": {
            "self": {
                "href": "/tournaments/aut_oc"
            },
            "seasons": {
                "href": "/tournaments/aut_oc/seasons/"
            }
        },
        "coverage": {
            "id": "aut",
            "name": "Austria",
            "_links": {
                "self": {
                    "href": "/territories/aut"
                }
            }
        },
        "season": {
            "name": "OFB Cup 2016/2017",
            "_links": {
                "self": {
                    "href": "/tournaments/aut_oc/seasons/20162017"
                }
            }
        },
        "teams_type": "club"
    }, {
        "id": "aut_tb",
        "name": "Tipico Bundesliga",
        "_links": {
            "self": {
                "href": "/tournaments/aut_tb"
            },
            "seasons": {
                "href": "/tournaments/aut_tb/seasons/"
            }
        },
        "coverage": {
            "id": "aut",
            "name": "Austria",
            "_links": {
                "self": {
                    "href": "/territories/aut"
                }
            }
        },
        "season": {
            "name": "Tipico Bundesliga 2016/2017",
            "_links": {
                "self": {
                    "href": "/tournaments/aut_tb/seasons/20162017"
                }
            }
        },
        "teams_type": "club"
    }, {
        "id": "bel_d2",
        "name": "Proximus League",
        "_links": {
            "self": {
                "href": "/tournaments/bel_d2"
            },
            "seasons": {
                "href": "/tournaments/bel_d2/seasons/"
            }
        },
        "coverage": {
            "id": "bel",
            "name": "Belgium",
            "_links": {
                "self": {
                    "href": "/territories/bel"
                }
            }
        },
        "season": {
            "name": "Proximus League 2016/2017",
            "_links": {
                "self": {
                    "href": "/tournaments/bel_d2/seasons/20162017"
                }
            }
        },
        "teams_type": "club"
    }
]
```
 

## Get Tournament by ID

```
    GET /v1/tournaments/:tournamentId
```

This API-call returns Tournament item by tournament ID passed in URI path.   

**Example:**
```
$ curl -i 'http://api.goalapi.com/v1/tournaments/aut_oc' -H "X-AUTH-APIKEY: xxx-xxxx-xxx"
```
```json
{
    "id": "aut_oc",
    "name": "OFB Cup",
    "_links": {
        "self": {
            "href": "/tournaments/aut_oc"
        },
        "seasons": {
            "href": "/tournaments/aut_oc/seasons/"
        }
    },
    "coverage": {
        "id": "aut",
        "name": "Austria",
        "_links": {
            "self": {
                "href": "/territories/aut"
            }
        }
    },
    "season": {
        "name": "OFB Cup 2016/2017",
        "_links": {
            "self": {
                "href": "/tournaments/aut_oc/seasons/20162017"
            }
        }
    },
    "teams_type": "club"
}
```

## Tournament properties explained
 
 Each Tournament item contains following properties:
 
   - `id` - Tournament unique identifier 
   - `name` - title of Tournament
   - `season` - current active Season of Tournament
   - `coverage` - Territory or array of Territories who's Teams can participate this Tournament   
   - `teams_type` - what kind of Teams can play in this Tournament; can be `club`, `national` and `generic`  
   - `_links` -  [HAL _links](/README.md#_links-attribute-for-each-item)
  

## Get Matches and other data from Tournament
 
 There is no way to get data about Matches, Teams, Players and Standings Tables by tournament ID. 
 In order to access that data, clients must go via `Seasons` and `Stages`. 
 
 The **Tournament** object itself just describes the competition, gives some description of what the competition is. 
 Tournament is just a _prototype_ of competition. 
 The concrete instances of any competition are `Seasons`. 
 
### Seasons
 
 The **Season** - is an object which represents some Tournament in certain time and place. 
 Each tournament object has _link to `seasons` API-call which will return all available Seasons for this Tournament. 

```
  GET /v1/tournaments/:tournamentId/seasons/
```
 
**Example:**
```
$ curl -i 'http://api.goalapi.com/v1/tournaments/aut_oc/seasons/' -H "X-AUTH-APIKEY: xxx-xxxx-xxx"
```
```json
[
    {
        "name": "OFB Cup 2016/2017",
        "_links": {
            "self": {
                "href": "/tournaments/aut_oc/seasons/20162017"
            }
        }
    },
    {
        "name": "OFB Cup 2015/2016",
        "_links": {
            "self": {
                "href": "/tournaments/aut_oc/seasons/20152016"
            }
        }
    },
    {
        "name": "OFB Cup 2014/2015",
        "_links": {
            "self": {
                "href": "/tournaments/aut_oc/seasons/20142015"
            }
        }
    }
]
```

Seasons can have Matches. 
    
```
    GET /v1/tournaments/:tournamentId/seasons/:seasonId/matches/
```

Each Team taking part in certain Season has a Squad - a list of Players supposed to play in Matches of Season.
    
```
  GET /v1/tournaments/:tournamentId/seasons/:seasonId/teams/
```


### Stages
 
 Each `Season` is divided to one or more `Stages`. The example of `Stages` inside some certain Champions League season can be _Qualification round_, _Group Stage_, _Playoffs Stage_.
 In order to access all Stages of particular Season, the client must make `stages` API-call 

```
    GET /v1/tournaments/:tournamentId/seasons/:seasonId/stages/
```
 
 To get data for some certain Stage clients can make API-calls with stage ID 

```
    GET /v1/tournaments/:tournamentId/seasons/:seasonId/stages/:stageId
```
 
 As well as for Seasons, for Stages it is also possible to get Matches and Teams
 
```
    GET /v1/tournaments/:tournamentId/seasons/:seasonId/stages/:stageId/matches/
       
    GET /v1/tournaments/:tournamentId/seasons/:seasonId/stages/:stageId/teams/
```
