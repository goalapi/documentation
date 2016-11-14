# Seasons and Stages
 

The **Season** - is an object which represents some Tournament in certain time and place. The concrete instances of any competition are Seasons. 
Each Season is divided to one or more Stages. Individual Stages may have their own competition scheme (round robin, playoff or other), standings tables and some other details.       
 
 
1. [List Tournament's Seasons](#list-tournaments-seasons)
1. [Get Season by ID](#get-season-by-id)
1. [List Season's Stages](#list-seasons-stages)
1. [Get Stage by ID](#get-stage-by-id)
1. [List Matches from Season or Stage](#matches)
1. [List Teams from Season or Stage](#teams)
1. [Teams Line Ups for Season or Stage](#teams-line-ups-for-season-or-stage)
1. [How to get Standings](#how-to-get-standings)


## List Tournament's Seasons

```
    GET /v1/tournaments/:tournamentId/seasons/
``` 


**Example:**
```bash
    $ curl -i 'http://api.goalapi.com/v1/tournaments/aut_oc/seasons/' -H "X-AUTH-APIKEY: xxx-xxxx-xxx"
 
    HTTP/1.1 200 OK
    Content-Type: application/json
    X-API-Version: 1
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
    }, {
        "name": "OFB Cup 2015/2016",
        "_links": {
            "self": {
                "href": "/tournaments/aut_oc/seasons/20152016"
            }
        }
    }, {
        "name": "OFB Cup 2014/2015",
        "_links": {
            "self": {
                "href": "/tournaments/aut_oc/seasons/20142015"
            }
        }
    }
]
```

Seasons and Stages do not have explicit IDs. For identification purposes clients may use value of `_links.self.href` attribute.
   
   
## Get Season by ID
```
    GET /v1/tournaments/:tournamentId/seasons/:seasonId
``` 


**Example:**
```bash
    $ curl -i 'http://api.goalapi.com/v1/tournaments/aut_oc/seasons/20162017' -H "X-AUTH-APIKEY: xxx-xxxx-xxx"
 
    HTTP/1.1 200 OK
    Content-Type: application/json
    X-API-Version: 1
```
```json
{
    "name": "OFB Cup 2016/2017",
    "_links": {
        "self": {
            "href": "/tournaments/aut_oc/seasons/20162017"
        },
        "stages": {
            "href": "/tournaments/aut_oc/seasons/20162017/stages/"
        },
        "matches": {
            "href": "/tournaments/aut_oc/seasons/20162017/matches/"
        }
    },
    "tournament": {
        "id": "aut_oc",
        "name": "Ofb Cup",
        "_links": {
            "self": {
                "href": "/tournaments/aut_oc"
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
        }
    },
    "stages": [
        {
            "name": "Main",
            "_links": {
                "self": {
                    "href": "/tournaments/aut_oc/seasons/20162017/stages/main"
                }
            }
        }
    ]
}
```


## List Season's Stages 

```
    GET /v1/tournaments/:tournamentId/seasons/:seasonId/stages/
``` 


**Example:**
```bash
    $ curl -i 'http://api.goalapi.com/v1/tournaments/cuefa/seasons/20152016/stages/' -H "X-AUTH-APIKEY: xxx-xxxx-xxx"
 
    HTTP/1.1 200 OK
    Content-Type: application/json
    X-API-Version: 1
```
```json
[
    {
        "name": "Group Stage",
        "_links": {
            "self": {
                "href": "/tournaments/cuefa/seasons/20152016/stages/groupstage"
            }
        }
    },
    {
        "name": "Play Offs",
        "_links": {
            "self": {
                "href": "/tournaments/cuefa/seasons/20152016/stages/playoffs"
            }
        }
    },
    {
        "name": "Qualification",
        "_links": {
            "self": {
                "href": "/tournaments/cuefa/seasons/20152016/stages/qualification"
            }
        }
    }
]
```


## Get Stage by ID
```
    GET /v1/tournaments/:tournamentId/seasons/:seasonId/stages/:stageId
``` 


**Example:**
```bash
    $ curl -i 'http://api.goalapi.com/v1/tournaments/cuefa/seasons/20152016/stages/groupstage' -H "X-AUTH-APIKEY: xxx-xxxx-xxx"
 
    HTTP/1.1 200 OK
    Content-Type: application/json
    X-API-Version: 1
```
```json
{
    "name": "Group Stage",
    "_links": {
        "self": {
            "href": "/tournaments/cuefa/seasons/20152016/stages/groupstage"
        },
        "standings": {
            "href": "/tournaments/cuefa/seasons/20152016/stages/groupstage/standings/"
        },
        "teams": {
            "href": "/tournaments/cuefa/seasons/20152016/stages/groupstage/teams/"
        },
        "matches": {
            "href": "/tournaments/cuefa/seasons/20152016/stages/groupstage/matches/"
        }
    },
    "tournament": {
        "id": "cuefa",
        "name": "Europa League",
        "_links": {
            "self": {
                "href": "/tournaments/cuefa"
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
        "name": "Europa League 2015/2016",
        "_links": {
            "self": {
                "href": "/tournaments/cuefa/seasons/20152016"
            }
        }
    }
}
```

## Matches 

GoalAPI-v1 provides ability to get Matches played in some Season or certain Stage of season. 
```
    GET /v1/tournaments/:tournamentId/seasons/:seasonId/matches/
    GET /v1/tournaments/:tournamentId/seasons/:seasonId/stages/:stageId/matches/
```

Full representation of Season or Stage contains link to `matches` API-calls which returns list of all Matches inside them.
The good practice is follow this link to get Matches.
```json
 {
     "_links": {
         "matches": {
             "href": "/tournaments/cuefa/seasons/20152016/stages/groupstage/matches/"
         }
     }
 }
``` 

More details about how to work with Matches [is here](./Matches.md)


## Teams 

Each Season or Stage has set of Teams which can differ from season to season and from stage to stage inside one season. 
In order to get lists of Teams for certain Season or Stage clients can use `teams` API-call

```
    GET /v1/tournaments/:tournamentId/seasons/:seasonId/teams/
    GET /v1/tournaments/:tournamentId/seasons/:seasonId/stages/:stageId/teams/
```

**Example:**
```bash
    $ curl -i 'http://api.goalapi.com/v1/tournaments/wor_wc/seasons/2014/stages/finaltournament.playoff/teams/' -H "X-AUTH-APIKEY: xxx-xxxx-xxx"
 
    HTTP/1.1 200 OK
    Content-Type: application/json
    X-API-Version: 1
```
```json
[
    {
        "id": "deu_nat",
        "name": "Germany",
        "_links": {
            "team": {
                "href": "/teams/deu_nat"
            },
            "self": {
                "href": "/tournaments/wor_wc/seasons/2014/stages/finaltournament.playoff/teams/deu_nat"
            }
        }
    },
    {
        "id": "nld_nat",
        "name": "Netherlands",
        "_links": {
            "team": {
                "href": "/teams/nld_nat"
            },
            "self": {
                "href": "/tournaments/wor_wc/seasons/2014/stages/finaltournament.playoff/teams/nld_nat"
            }
        }
    },
    {
        "id": "cri_nat",
        "name": "Costa Rica",
        "_links": {
            "team": {
                "href": "/teams/cri_nat"
            },
            "self": {
                "href": "/tournaments/wor_wc/seasons/2014/stages/finaltournament.playoff/teams/cri_nat"
            }
        }
    }
]
```

## Teams Line Ups for Season or Stage
It is possible to get list of Players for each Team taking part in competition. Teams may have different list of Players. 
Players can change their Teams in different Seasons or even in one season. 
In order to see which Players played for specified Team inside certain Season or Stage clients cam do `team` API-call
  
```
    GET /v1/tournaments/:tournamentId/seasons/:seasonId/teams/:teamId
    GET /v1/tournaments/:tournamentId/seasons/:seasonId/stages/:stageId/teams/:teamId
```

**Example:**
```bash
    $ curl -i 'http://api.goalapi.com/v1/tournaments/wor_wc/seasons/2014/stages/finaltournament.playoff/teams/cri_nat' -H "X-AUTH-APIKEY: xxx-xxxx-xxx"
 
    HTTP/1.1 200 OK
    Content-Type: application/json
    X-API-Version: 1
```
```json
{
    "id": "cri_nat",
    "name": "Costa Rica",
    "_links": {
        "team": {
            "href": "/teams/cri_nat"
        },
        "self": {
            "href": "/tournaments/wor_wc/seasons/2014/stages/finaltournament.playoff/teams/cri_nat"
        }
    },
    "tournament": {
        "id": "wor_wc",
        "name": "World Cup",
        "_links": {
            "self": {
                "href": "/tournaments/wor_wc"
            }
        },
        "coverage": {
            "id": "world",
            "name": "Worldwide",
            "_links": {
                "self": {
                    "href": "/territories/world"
                }
            }
        }
    },
    "season": {
        "name": "World Cup 2014",
        "_links": {
            "self": {
                "href": "/tournaments/wor_wc/seasons/2014"
            }
        }
    },
    "players": [
        {
            "id": "acosta-johnny",
            "name": "Acosta Johnny",
            "_links": {
                "self": {
                    "href": "/players/acosta-johnny"
                }
            },
            "number": 2
        },
        {
            "id": "bolanos-christian",
            "name": "Bolanos Christian",
            "_links": {
                "self": {
                    "href": "/players/bolanos-christian"
                }
            },
            "number": 7
        },
        {
            "id": "borges-celso",
            "name": "Borges Celso",
            "_links": {
                "self": {
                    "href": "/players/borges-celso"
                }
            },
            "number": 5
        }
    ],
    "stage": {
        "name": "Play Offs",
        "_links": {
            "self": {
                "href": "/tournaments/wor_wc/seasons/2014/stages/finaltournament.playoff"
            }
        }
    }
}
```




## How to get Standings

Some Stages may have standings tables. In case if Stage has, `_links` attribute will have `standings` field with link to `standings` API-call. 

```
    GET /v1/tournaments/:tournamentId/seasons/:seasonId/stages/:stageId/standings/
```

More details about Standings Tables [is here](./Standings.md).

**Example:**
```json
 {
     "_links": {
         "standings": {
             "href": "/tournaments/cuefa/seasons/20152016/stages/groupstage/standings/"
         }
     }
 }
```