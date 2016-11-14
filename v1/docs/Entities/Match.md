# Matches
This describes API-calls to fetch Matches

1. [List Matches from particular Season or Stage](#list-matches-from-particular-season-or-stage)
    - [Pagination](#matches-pagination)
1. [Get Match by ID](#get-match-by-id)
1. [List online Matches](#list-online-matches)
1. [Match properties explained](Match/properties.md#match-properties-explained)

## List Matches from particular Season or Stage

```
GET /v1/tournaments/:tournamentId/seasons/:seasonId/matches/:page/
GET /v1/tournaments/:tournamentId/seasons/:seasonId/stages/:stageId/matches/:page/
```

Lists all matches from Season or Stage specified in path. These API-calls returns array of items, each item represents summary of Match. Summaries DO NOT include info about Teams Lineups and Match Events (like goals, cards, etc...).

**Example:**
```
$ curl -i 'http://api.goalapi.com/v1/tournaments/eng_pl/seasons/20162017/matches/1/' -H "X-AUTH-APIKEY: xxx-xxxx-xxx"

HTTP/1.1 200 OK
Content-Type: application/json
X-API-Version: 1
X-Total-Count: 380
X-First-Index: 128
X-Last-Index: 255
Link: </v1/tournaments/eng_pl/seasons/20162017/matches/>; rel="prev",  </v1/tournaments/eng_pl/seasons/20162017/matches/3/>; rel="next"
```
```json
[
    {
        "id": "5770bf3743fdd778976e4300eb8e5881",
        "begin_time": {
            "date_time": "2016-09-25T15:00:00+00:00",
            "timestamp": 1474815600
        },
        "status": {
            "status": "finished",
            "score": [
                0,
                3
            ],
            "finished_after": "2T"
        },
        "tournament": {
            "id": "eng_pl",
            "name": "Premier League",
            "_links": {
                "self": {
                    "href": "/tournaments/eng_pl"
                }
            },
            "coverage": {
                "id": "eng",
                "name": "England",
                "_links": {
                    "self": {
                        "href": "/territories/eng"
                    }
                }
            }
        },
        "teams": [
            {
                "id": "wesham_eng",
                "name": "West Ham",
                "_links": {
                    "self": {
                        "href": "/teams/wesham_eng"
                    }
                }
            },
            {
                "id": "sou_eng",
                "name": "Southampton",
                "_links": {
                    "self": {
                        "href": "/teams/sou_eng"
                    }
                }
            }
        ],
        "season": {
            "name": "Premier League 2016/2017",
            "_links": {
                "self": {
                    "href": "/tournaments/eng_pl/seasons/20162017"
                }
            }
        },
        "stage": {
            "name": "Main",
            "_links": {
                "self": {
                    "href": "/tournaments/eng_pl/seasons/20162017/stages/main"
                }
            }
        },
        "_links": {
            "self": {
                "href": "/tournaments/eng_pl/seasons/20162017/matches/5770bf3743fdd778976e4300eb8e5881"
            }
        },
        "context": {
            "matchday": "Round 6"
        },
        "last_update_time": {
            "date_time": "2016-09-25T16:56:04+00:00",
            "timestamp": 1474822564
        }
    },
    {
        "id": "e6928e1eba4338b51b248c4c32712cc8",
        "begin_time": {
            "date_time": "2016-09-26T19:00:00+00:00",
            "timestamp": 1474916400
        },
        "status": {
            "status": "finished",
            "score": [
                2,
                0
            ],
            "finished_after": "2T"
        },
        "tournament": {
            "id": "eng_pl",
            "name": "Premier League",
            "_links": {
                "self": {
                    "href": "/tournaments/eng_pl"
                }
            },
            "coverage": {
                "id": "eng",
                "name": "England",
                "_links": {
                    "self": {
                        "href": "/territories/eng"
                    }
                }
            }
        },
        "teams": [
            {
                "id": "bur_eng",
                "name": "Burnley",
                "_links": {
                    "self": {
                        "href": "/teams/bur_eng"
                    }
                }
            },
            {
                "id": "wat_eng",
                "name": "Watford",
                "_links": {
                    "self": {
                        "href": "/teams/wat_eng"
                    }
                }
            }
        ],
        "season": {
            "name": "Premier League 2016/2017",
            "_links": {
                "self": {
                    "href": "/tournaments/eng_pl/seasons/20162017"
                }
            }
        },
        "stage": {
            "name": "Main",
            "_links": {
                "self": {
                    "href": "/tournaments/eng_pl/seasons/20162017/stages/main"
                }
            }
        },
        "_links": {
            "self": {
                "href": "/tournaments/eng_pl/seasons/20162017/matches/e6928e1eba4338b51b248c4c32712cc8"
            }
        },
        "context": {
            "matchday": "Round 6"
        },
        "last_update_time": {
            "date_time": "2016-09-26T20:54:03+00:00",
            "timestamp": 1474923243
        }
    }
]
```
### Matches pagination
Matches API-calls designed to return arrays of items and they have to return too many items. 
In order to reduce possible heaviness of such requests we added pagination. 
This means that each API-call for List of Matches must have `page` parameter in the end of URI path 

```
$ curl -i  'http://api.goalapi.com/v1/tournaments/eng_pl/seasons/20162017/matches/2/' -H "X-AUTH-APIKEY: xxx-xxxx-xxx"

HTTP/1.1 200 OK
Content-Type: application/json
X-Total-Count: 380
X-First-Index: 128
X-Last-Index: 255
Link: </v1/tournaments/eng_pl/seasons/20162017/matches/1/>; rel="prev",  </v1/tournaments/eng_pl/seasons/20162017/matches/3/>; rel="next"
```

Paginated responses contains additional fields in header: `Link`, `X-Total-Count`, `X-First-Index`, `X-Last-Index`. 
 
 * `Link` contains list of links which must be used to access next or previous pages
 * `X-Total-Count` - is a maximum number Matches inside specified Season or Stage
 * `X-First-Index` - numeric index of first item in current portion of Matches
 * `X-Last-Index` - numeric index of last item in current portion of Matches


## Get Match by ID

```
GET /tournaments/:tournamentId/seasons/:seasonId/matches/:matchId
GET /tournaments/:tournamentId/seasons/:seasonId/stages/:stageId/matches/:matchId
```

Returns one Match by **matchId** from Season or Stage specified in path. These API-calls return one Match with full details i.e with Events and Team lineups if available.  

**Example:**
```
$ curl -i  'http://api.goalapi.com/v1/tournaments/eng_pl/seasons/20162017/matches/a2febee5b50e835c9efd14952bb8206f' -H "X-AUTH-APIKEY: xxx-xxxx-xxx"

HTTP/1.1 200 OK
Content-Type: application/json
X-API-Version: 1
```

```json
{
    "id": "a2febee5b50e835c9efd14952bb8206f",
    "begin_time": {
        "date_time": "2016-08-13T14:00:00+00:00",
        "timestamp": 1471096800
    },
    "status": {
        "status": "finished",
        "score": [
            1,
            1
        ],
        "finished_after": "2T"
    },
    "tournament": {
        "id": "eng_pl",
        "name": "Premier League",
        "_links": {
            "self": {
                "href": "/tournaments/eng_pl"
            }
        },
        "coverage": {
            "id": "eng",
            "name": "England",
            "_links": {
                "self": {
                    "href": "/territories/eng"
                }
            }
        }
    },
    "teams": [
        {
            "id": "sou_eng",
            "name": "Southampton",
            "_links": {
                "self": {
                    "href": "/teams/sou_eng"
                }
            },
            "squad": {
                "eleven": [
                    {
                        "id": "cedric-alves",
                        "name": "Cedric Alves",
                        "_links": {
                            "self": {
                                "href": "/players/cedric-alves"
                            }
                        },
                        "number": 2
                    },
                    {
                        "id": "davis-steven",
                        "name": "Davis Steven",
                        "_links": {
                            "self": {
                                "href": "/players/davis-steven"
                            }
                        },
                        "number": 8,
                        "captain": true
                    },
                    {
                        "id": "forster-fraser",
                        "name": "Forster Fraser",
                        "_links": {
                            "self": {
                                "href": "/players/forster-fraser"
                            }
                        },
                        "number": 1,
                        "role": "goalkeeper"
                    },
                    {
                        "id": "long-shane",
                        "name": "Long Shane",
                        "_links": {
                            "self": {
                                "href": "/players/long-shane"
                            }
                        },
                        "number": 7
                    },
                    {
                        "id": "redmond-nathan",
                        "name": "Redmond Nathan",
                        "_links": {
                            "self": {
                                "href": "/players/redmond-nathan"
                            }
                        },
                        "number": 22
                    },
                    {
                        "id": "romeu-oriol",
                        "name": "Romeu Oriol",
                        "_links": {
                            "self": {
                                "href": "/players/romeu-oriol"
                            }
                        },
                        "number": 14
                    },
                    {
                        "id": "tadic-dusan",
                        "name": "Tadic Dusan",
                        "_links": {
                            "self": {
                                "href": "/players/tadic-dusan"
                            }
                        },
                        "number": 11
                    },
                    {
                        "id": "targett-matt",
                        "name": "Targett Matt",
                        "_links": {
                            "self": {
                                "href": "/players/targett-matt"
                            }
                        },
                        "number": 33
                    },
                    {
                        "id": "van-dijk-virgil",
                        "name": "Van Dijk Virgil",
                        "_links": {
                            "self": {
                                "href": "/players/van-dijk-virgil"
                            }
                        },
                        "number": 17
                    },
                    {
                        "id": "ward-prowse-james",
                        "name": "Ward Prowse James",
                        "_links": {
                            "self": {
                                "href": "/players/ward-prowse-james"
                            }
                        },
                        "number": 16
                    },
                    {
                        "id": "yoshida-maya",
                        "name": "Yoshida Maya",
                        "_links": {
                            "self": {
                                "href": "/players/yoshida-maya"
                            }
                        },
                        "number": 3
                    }
                ],
                "substitutions": [
                    {
                        "id": "austin-charlie",
                        "name": "Austin Charlie",
                        "_links": {
                            "self": {
                                "href": "/players/austin-charlie"
                            }
                        },
                        "number": 10
                    },
                    {
                        "id": "clasie-jordy",
                        "name": "Clasie Jordy",
                        "_links": {
                            "self": {
                                "href": "/players/clasie-jordy"
                            }
                        },
                        "number": 4
                    },
                    {
                        "id": "fonte-jose",
                        "name": "Fonte Jose",
                        "_links": {
                            "self": {
                                "href": "/players/fonte-jose"
                            }
                        },
                        "number": 6
                    },
                    {
                        "id": "hojbjerg-pierre-emile",
                        "name": "Hojbjerg Pierre Emile",
                        "_links": {
                            "self": {
                                "href": "/players/hojbjerg-pierre-emile"
                            }
                        },
                        "number": 23
                    },
                    {
                        "id": "mccarthy-alex",
                        "name": "Mccarthy Alex",
                        "_links": {
                            "self": {
                                "href": "/players/mccarthy-alex"
                            }
                        },
                        "number": 13,
                        "role": "goalkeeper"
                    },
                    {
                        "id": "pied-jeremy",
                        "name": "Pied Jeremy",
                        "_links": {
                            "self": {
                                "href": "/players/pied-jeremy"
                            }
                        },
                        "number": 26
                    },
                    {
                        "id": "rodriguez-jay",
                        "name": "Rodriguez Jay",
                        "_links": {
                            "self": {
                                "href": "/players/rodriguez-jay"
                            }
                        },
                        "number": 9
                    }
                ]
            }
        },
        {
            "id": "wat_eng",
            "name": "Watford",
            "_links": {
                "self": {
                    "href": "/teams/wat_eng"
                }
            },
            "squad": {
                "eleven": [
                    {
                        "id": "amrabat-nordin",
                        "name": "Amrabat Nordin",
                        "_links": {
                            "self": {
                                "href": "/players/amrabat-nordin"
                            }
                        },
                        "number": 7
                    },
                    {
                        "id": "behrami-valon",
                        "name": "Behrami Valon",
                        "_links": {
                            "self": {
                                "href": "/players/behrami-valon"
                            }
                        },
                        "number": 11
                    },
                    {
                        "id": "britos-miguel",
                        "name": "Britos Miguel",
                        "_links": {
                            "self": {
                                "href": "/players/britos-miguel"
                            }
                        },
                        "number": 3
                    },
                    {
                        "id": "capoue-etienne",
                        "name": "Capoue Etienne",
                        "_links": {
                            "self": {
                                "href": "/players/capoue-etienne"
                            }
                        },
                        "number": 29
                    },
                    {
                        "id": "cathcart-craig",
                        "name": "Cathcart Craig",
                        "_links": {
                            "self": {
                                "href": "/players/cathcart-craig"
                            }
                        },
                        "number": 15
                    },
                    {
                        "id": "deeney-troy",
                        "name": "Deeney Troy",
                        "_links": {
                            "self": {
                                "href": "/players/deeney-troy"
                            }
                        },
                        "number": 9,
                        "captain": true
                    },
                    {
                        "id": "gomes-heurelho",
                        "name": "Gomes Heurelho",
                        "_links": {
                            "self": {
                                "href": "/players/gomes-heurelho"
                            }
                        },
                        "number": 1,
                        "role": "goalkeeper"
                    },
                    {
                        "id": "guedioura-adlene",
                        "name": "Guedioura Adlene",
                        "_links": {
                            "self": {
                                "href": "/players/guedioura-adlene"
                            }
                        },
                        "number": 17
                    },
                    {
                        "id": "holebas-jose",
                        "name": "Holebas Jose",
                        "_links": {
                            "self": {
                                "href": "/players/holebas-jose"
                            }
                        },
                        "number": 25
                    },
                    {
                        "id": "ighalo-odion",
                        "name": "Ighalo Odion",
                        "_links": {
                            "self": {
                                "href": "/players/ighalo-odion"
                            }
                        },
                        "number": 24
                    },
                    {
                        "id": "prodl-sebastian",
                        "name": "Prodl Sebastian",
                        "_links": {
                            "self": {
                                "href": "/players/prodl-sebastian"
                            }
                        },
                        "number": 5
                    }
                ],
                "substitutions": [
                    {
                        "id": "anya-ikechi",
                        "name": "Anya Ikechi",
                        "_links": {
                            "self": {
                                "href": "/players/anya-ikechi"
                            }
                        },
                        "number": 21
                    },
                    {
                        "id": "nyom-allan",
                        "name": "Nyom Allan",
                        "_links": {
                            "self": {
                                "href": "/players/nyom-allan"
                            }
                        },
                        "number": 2
                    },
                    {
                        "id": "pantilimon-costel",
                        "name": "Pantilimon Costel",
                        "_links": {
                            "self": {
                                "href": "/players/pantilimon-costel"
                            }
                        },
                        "number": 30,
                        "role": "goalkeeper"
                    },
                    {
                        "id": "sinclair-jerome",
                        "name": "Sinclair Jerome",
                        "_links": {
                            "self": {
                                "href": "/players/sinclair-jerome"
                            }
                        },
                        "number": 19
                    },
                    {
                        "id": "vydra-matej",
                        "name": "Vydra Matej",
                        "_links": {
                            "self": {
                                "href": "/players/vydra-matej"
                            }
                        },
                        "number": 20
                    },
                    {
                        "id": "watson-ben",
                        "name": "Watson Ben",
                        "_links": {
                            "self": {
                                "href": "/players/watson-ben"
                            }
                        },
                        "number": 23
                    },
                    {
                        "id": "zuniga-juan",
                        "name": "Zuniga Juan",
                        "_links": {
                            "self": {
                                "href": "/players/zuniga-juan"
                            }
                        },
                        "number": 18
                    }
                ]
            }
        }
    ],
    "season": {
        "name": "Premier League 2016/2017",
        "_links": {
            "self": {
                "href": "/tournaments/eng_pl/seasons/20162017"
            }
        }
    },
    "stage": {
        "name": "Main",
        "_links": {
            "self": {
                "href": "/tournaments/eng_pl/seasons/20162017/stages/main"
            }
        }
    },
    "_links": {
        "self": {
            "href": "/tournaments/eng_pl/seasons/20162017/matches/a2febee5b50e835c9efd14952bb8206f"
        }
    },
    "context": {
        "matchday": "Round 1"
    },
    "last_update_time": {
        "date_time": "2016-09-05T06:12:03+00:00",
        "timestamp": 1473055923
    },
    "events": [
        {
            "type": "goal",
            "team": {
                "id": "wat_eng",
                "name": "Watford",
                "_links": {
                    "self": {
                        "href": "/teams/wat_eng"
                    }
                }
            },
            "moment": {
                "period": "1T",
                "moment": {
                    "minute": 9
                }
            },
            "player": {
                "id": "capoue-etienne",
                "name": "Capoue Etienne",
                "_links": {
                    "self": {
                        "href": "/players/capoue-etienne"
                    }
                }
            },
            "score": [
                0,
                1
            ]
        },
        {
            "type": "substitution",
            "team": {
                "id": "sou_eng",
                "name": "Southampton",
                "_links": {
                    "self": {
                        "href": "/teams/sou_eng"
                    }
                }
            },
            "moment": {
                "period": "2T",
                "moment": {
                    "minute": 55
                }
            },
            "players": {
                "in": {
                    "id": "hojbjerg-pierre-emile",
                    "name": "Hojbjerg Pierre Emile",
                    "_links": {
                        "self": {
                            "href": "/players/hojbjerg-pierre-emile"
                        }
                    }
                },
                "out": {
                    "id": "ward-prowse-james",
                    "name": "Ward Prowse James",
                    "_links": {
                        "self": {
                            "href": "/players/ward-prowse-james"
                        }
                    }
                }
            }
        },
        {
            "type": "goal",
            "team": {
                "id": "sou_eng",
                "name": "Southampton",
                "_links": {
                    "self": {
                        "href": "/teams/sou_eng"
                    }
                }
            },
            "moment": {
                "period": "2T",
                "moment": {
                    "minute": 58
                }
            },
            "player": {
                "id": "redmond-nathan",
                "name": "Redmond Nathan",
                "_links": {
                    "self": {
                        "href": "/players/redmond-nathan"
                    }
                }
            },
            "score": [
                1,
                1
            ]
        },
        {
            "type": "card",
            "team": {
                "id": "wat_eng",
                "name": "Watford",
                "_links": {
                    "self": {
                        "href": "/teams/wat_eng"
                    }
                }
            },
            "moment": {
                "period": "2T",
                "moment": {
                    "minute": 60
                }
            },
            "color": "yellow",
            "player": {
                "id": "guedioura-adlene",
                "name": "Guedioura Adlene",
                "_links": {
                    "self": {
                        "href": "/players/guedioura-adlene"
                    }
                }
            }
        },
        {
            "type": "substitution",
            "team": {
                "id": "wat_eng",
                "name": "Watford",
                "_links": {
                    "self": {
                        "href": "/teams/wat_eng"
                    }
                }
            },
            "moment": {
                "period": "2T",
                "moment": {
                    "minute": 64
                }
            },
            "players": {
                "in": {
                    "id": "watson-ben",
                    "name": "Watson Ben",
                    "_links": {
                        "self": {
                            "href": "/players/watson-ben"
                        }
                    }
                },
                "out": {
                    "id": "behrami-valon",
                    "name": "Behrami Valon",
                    "_links": {
                        "self": {
                            "href": "/players/behrami-valon"
                        }
                    }
                }
            }
        },
        {
            "type": "substitution",
            "team": {
                "id": "wat_eng",
                "name": "Watford",
                "_links": {
                    "self": {
                        "href": "/teams/wat_eng"
                    }
                }
            },
            "moment": {
                "period": "2T",
                "moment": {
                    "minute": 73
                }
            },
            "players": {
                "in": {
                    "id": "zuniga-juan",
                    "name": "Zuniga Juan",
                    "_links": {
                        "self": {
                            "href": "/players/zuniga-juan"
                        }
                    }
                },
                "out": {
                    "id": "guedioura-adlene",
                    "name": "Guedioura Adlene",
                    "_links": {
                        "self": {
                            "href": "/players/guedioura-adlene"
                        }
                    }
                }
            }
        },
        {
            "type": "card",
            "team": {
                "id": "wat_eng",
                "name": "Watford",
                "_links": {
                    "self": {
                        "href": "/teams/wat_eng"
                    }
                }
            },
            "moment": {
                "period": "2T",
                "moment": {
                    "minute": 76
                }
            },
            "color": "red",
            "player": {
                "id": "watson-ben",
                "name": "Watson Ben",
                "_links": {
                    "self": {
                        "href": "/players/watson-ben"
                    }
                }
            }
        },
        {
            "type": "substitution",
            "team": {
                "id": "sou_eng",
                "name": "Southampton",
                "_links": {
                    "self": {
                        "href": "/teams/sou_eng"
                    }
                }
            },
            "moment": {
                "period": "2T",
                "moment": {
                    "minute": 80
                }
            },
            "players": {
                "in": {
                    "id": "pied-jeremy",
                    "name": "Pied Jeremy",
                    "_links": {
                        "self": {
                            "href": "/players/pied-jeremy"
                        }
                    }
                },
                "out": {
                    "id": "cedric-alves",
                    "name": "Cedric Alves",
                    "_links": {
                        "self": {
                            "href": "/players/cedric-alves"
                        }
                    }
                }
            }
        },
        {
            "type": "substitution",
            "team": {
                "id": "wat_eng",
                "name": "Watford",
                "_links": {
                    "self": {
                        "href": "/teams/wat_eng"
                    }
                }
            },
            "moment": {
                "period": "2T",
                "moment": {
                    "minute": 81
                }
            },
            "players": {
                "in": {
                    "id": "anya-ikechi",
                    "name": "Anya Ikechi",
                    "_links": {
                        "self": {
                            "href": "/players/anya-ikechi"
                        }
                    }
                },
                "out": {
                    "id": "ighalo-odion",
                    "name": "Ighalo Odion",
                    "_links": {
                        "self": {
                            "href": "/players/ighalo-odion"
                        }
                    }
                }
            }
        },
        {
            "type": "substitution",
            "team": {
                "id": "sou_eng",
                "name": "Southampton",
                "_links": {
                    "self": {
                        "href": "/teams/sou_eng"
                    }
                }
            },
            "moment": {
                "period": "2T",
                "moment": {
                    "minute": 83
                }
            },
            "players": {
                "in": {
                    "id": "austin-charlie",
                    "name": "Austin Charlie",
                    "_links": {
                        "self": {
                            "href": "/players/austin-charlie"
                        }
                    }
                },
                "out": {
                    "id": "long-shane",
                    "name": "Long Shane",
                    "_links": {
                        "self": {
                            "href": "/players/long-shane"
                        }
                    }
                }
            }
        },
        {
            "type": "card",
            "team": {
                "id": "wat_eng",
                "name": "Watford",
                "_links": {
                    "self": {
                        "href": "/teams/wat_eng"
                    }
                }
            },
            "moment": {
                "period": "2T",
                "moment": {
                    "minute": 87
                }
            },
            "color": "yellow",
            "player": {
                "id": "gomes-heurelho",
                "name": "Gomes Heurelho",
                "_links": {
                    "self": {
                        "href": "/players/gomes-heurelho"
                    }
                }
            }
        },
        {
            "type": "card",
            "team": {
                "id": "sou_eng",
                "name": "Southampton",
                "_links": {
                    "self": {
                        "href": "/teams/sou_eng"
                    }
                }
            },
            "moment": {
                "period": "2T",
                "moment": {
                    "minute": 94
                }
            },
            "color": "yellow",
            "player": {
                "id": "van-dijk-virgil",
                "name": "Van Dijk Virgil",
                "_links": {
                    "self": {
                        "href": "/players/van-dijk-virgil"
                    }
                }
            }
        }
    ]
}
```

## List online Matches

```
GET /v1/matches/now
```
Lists Matches which are online now, supposed to start within next several minutes or finished not so long ago. 
Matches are taken from Tournaments available for Subscription identified by API-key passed with the request. 
This API-call returns matches with all details including Events and Lineups. 

**Example:**
```
$ curl -i 'http://api.goalapi.com/v1/matches/now/' -H "X-AUTH-APIKEY: xxx-xxxx-xxx"

HTTP/1.1 200 OK
Content-Type: application/json
X-API-Version: 1
X-Total-Count:4
```
```json
[
    {
        "id": "51bcf895296312311248f8a728e6497e",
        "begin_time": {
            "date_time": "2016-11-13T11:00:00+00:00",
            "timestamp": 1479034800
        },
        "status": {
            "status": "online",
            "score": [
                0,
                0
            ],
            "period": "1T",
            "period_finish_time": {
                "date_time": "2016-11-13T11:48:02+00:00",
                "timestamp": 1479037682
            }
        },
        "tournament": {
            "id": "rus_d1",
            "name": "Division 1",
            "_links": {
                "self": {
                    "href": "/tournaments/rus_d1"
                }
            },
            "coverage": {
                "id": "rus",
                "name": "Russia",
                "_links": {
                    "self": {
                        "href": "/territories/rus"
                    }
                }
            }
        },
        "teams": [
            {
                "id": "spamos2_rus",
                "name": "Spartak Moscow 2",
                "_links": {
                    "self": {
                        "href": "/teams/spamos2_rus"
                    }
                },
                "squad": {
                    "eleven": [
                        {
                            "id": "filippov-mikhail",
                            "name": "Filippov Mikhail",
                            "_links": {
                                "self": {
                                    "href": "/players/filippov-mikhail"
                                }
                            },
                            "number": 30,
                            "role": "goalkeeper"
                        },
                        {
                            "id": "davydov-denis",
                            "name": "Davydov Denis",
                            "_links": {
                                "self": {
                                    "href": "/players/davydov-denis"
                                }
                            },
                            "number": 69
                        },
                        {
                            "id": "khomukha-ivan",
                            "name": "Khomukha Ivan",
                            "_links": {
                                "self": {
                                    "href": "/players/khomukha-ivan"
                                }
                            },
                            "number": 80
                        },
                        {
                            "id": "kutin-denis",
                            "name": "Kutin Denis",
                            "_links": {
                                "self": {
                                    "href": "/players/kutin-denis"
                                }
                            },
                            "number": 64
                        },
                        {
                            "id": "leontjev-igor",
                            "name": "Leontjev Igor",
                            "_links": {
                                "self": {
                                    "href": "/players/leontjev-igor"
                                }
                            },
                            "number": 52
                        },
                        {
                            "id": "melkadze-georgi",
                            "name": "Melkadze Georgi",
                            "_links": {
                                "self": {
                                    "href": "/players/melkadze-georgi"
                                }
                            },
                            "number": 37
                        },
                        {
                            "id": "putsko-aleksandr",
                            "name": "Putsko Aleksandr",
                            "_links": {
                                "self": {
                                    "href": "/players/putsko-aleksandr"
                                }
                            },
                            "number": 45
                        },
                        {
                            "id": "samsonov-artem",
                            "name": "Samsonov Artem",
                            "_links": {
                                "self": {
                                    "href": "/players/samsonov-artem"
                                }
                            },
                            "number": 53,
                            "captain": true
                        },
                        {
                            "id": "shinozuka-ippei",
                            "name": "Shinozuka Ippei",
                            "_links": {
                                "self": {
                                    "href": "/players/shinozuka-ippei"
                                }
                            },
                            "number": 39
                        },
                        {
                            "id": "timofeev-artem",
                            "name": "Timofeev Artem",
                            "_links": {
                                "self": {
                                    "href": "/players/timofeev-artem"
                                }
                            },
                            "number": 40
                        },
                        {
                            "id": "zuev-alexander",
                            "name": "Zuev Alexander",
                            "_links": {
                                "self": {
                                    "href": "/players/zuev-alexander"
                                }
                            },
                            "number": 17
                        }
                    ],
                    "substitutions": [
                        {
                            "id": "denisovich-artem",
                            "name": "Denisovich Artem",
                            "_links": {
                                "self": {
                                    "href": "/players/denisovich-artem"
                                }
                            },
                            "number": 93
                        },
                        {
                            "id": "fedchuk-artem",
                            "name": "Fedchuk Artem",
                            "_links": {
                                "self": {
                                    "href": "/players/fedchuk-artem"
                                }
                            },
                            "number": 67
                        },
                        {
                            "id": "panteleev-vladislav",
                            "name": "Panteleev Vladislav",
                            "_links": {
                                "self": {
                                    "href": "/players/panteleev-vladislav"
                                }
                            },
                            "number": 83
                        },
                        {
                            "id": "poluboyarinov-daniil",
                            "name": "Poluboyarinov Daniil",
                            "_links": {
                                "self": {
                                    "href": "/players/poluboyarinov-daniil"
                                }
                            },
                            "number": 97
                        },
                        {
                            "id": "rudenko-alexander",
                            "name": "Rudenko Alexander",
                            "_links": {
                                "self": {
                                    "href": "/players/rudenko-alexander"
                                }
                            },
                            "number": 79
                        },
                        {
                            "id": "shcherbakov-konstantin",
                            "name": "Shcherbakov Konstantin",
                            "_links": {
                                "self": {
                                    "href": "/players/shcherbakov-konstantin"
                                }
                            },
                            "number": 22
                        },
                        {
                            "id": "tereshkin-vladislav",
                            "name": "Tereshkin Vladislav",
                            "_links": {
                                "self": {
                                    "href": "/players/tereshkin-vladislav"
                                }
                            },
                            "number": 85,
                            "role": "goalkeeper"
                        }
                    ]
                }
            },
            {
                "id": "fvor_rus",
                "name": "F. Voronezh",
                "_links": {
                    "self": {
                        "href": "/teams/fvor_rus"
                    }
                },
                "squad": {
                    "eleven": [
                        {
                            "id": "sautin-aleksandr",
                            "name": "Sautin Aleksandr",
                            "_links": {
                                "self": {
                                    "href": "/players/sautin-aleksandr"
                                }
                            },
                            "number": 1,
                            "role": "goalkeeper"
                        },
                        {
                            "id": "alshin-ilnur",
                            "name": "Alshin Ilnur",
                            "_links": {
                                "self": {
                                    "href": "/players/alshin-ilnur"
                                }
                            },
                            "number": 10
                        },
                        {
                            "id": "bagaev-mikhail",
                            "name": "Bagaev Mikhail",
                            "_links": {
                                "self": {
                                    "href": "/players/bagaev-mikhail"
                                }
                            },
                            "number": 71
                        },
                        {
                            "id": "biryukov-mikhail",
                            "name": "Biryukov Mikhail",
                            "_links": {
                                "self": {
                                    "href": "/players/biryukov-mikhail"
                                }
                            },
                            "number": 17
                        },
                        {
                            "id": "burnash-georgy",
                            "name": "Burnash Georgy",
                            "_links": {
                                "self": {
                                    "href": "/players/burnash-georgy"
                                }
                            },
                            "number": 93
                        },
                        {
                            "id": "drannikov-ivan",
                            "name": "Drannikov Ivan",
                            "_links": {
                                "self": {
                                    "href": "/players/drannikov-ivan"
                                }
                            },
                            "number": 22
                        },
                        {
                            "id": "murnin-andrey",
                            "name": "Murnin Andrey",
                            "_links": {
                                "self": {
                                    "href": "/players/murnin-andrey"
                                }
                            },
                            "number": 7,
                            "captain": true
                        },
                        {
                            "id": "osipenko-maksim",
                            "name": "Osipenko Maksim",
                            "_links": {
                                "self": {
                                    "href": "/players/osipenko-maksim"
                                }
                            },
                            "number": 55
                        },
                        {
                            "id": "satalkin-nikita",
                            "name": "Satalkin Nikita",
                            "_links": {
                                "self": {
                                    "href": "/players/satalkin-nikita"
                                }
                            },
                            "number": 87
                        },
                        {
                            "id": "tikhiy-dmitriy",
                            "name": "Tikhiy Dmitriy",
                            "_links": {
                                "self": {
                                    "href": "/players/tikhiy-dmitriy"
                                }
                            },
                            "number": 27
                        },
                        {
                            "id": "troshechkin-aleksandr",
                            "name": "Troshechkin Aleksandr",
                            "_links": {
                                "self": {
                                    "href": "/players/troshechkin-aleksandr"
                                }
                            },
                            "number": 8
                        }
                    ],
                    "substitutions": [
                        {
                            "id": "bolov-ruslan",
                            "name": "Bolov Ruslan",
                            "_links": {
                                "self": {
                                    "href": "/players/bolov-ruslan"
                                }
                            },
                            "number": 77
                        },
                        {
                            "id": "ivanov-dmitri",
                            "name": "Ivanov Dmitri",
                            "_links": {
                                "self": {
                                    "href": "/players/ivanov-dmitri"
                                }
                            },
                            "number": 5
                        },
                        {
                            "id": "kozlov-aleksandr",
                            "name": "Kozlov Aleksandr",
                            "_links": {
                                "self": {
                                    "href": "/players/kozlov-aleksandr"
                                }
                            },
                            "number": 49
                        },
                        {
                            "id": "melnicenko-vitalijs",
                            "name": "Melnicenko Vitalijs",
                            "_links": {
                                "self": {
                                    "href": "/players/melnicenko-vitalijs"
                                }
                            },
                            "number": 88,
                            "role": "goalkeeper"
                        },
                        {
                            "id": "michurenkov-dmitri",
                            "name": "Michurenkov Dmitri",
                            "_links": {
                                "self": {
                                    "href": "/players/michurenkov-dmitri"
                                }
                            },
                            "number": 19
                        },
                        {
                            "id": "nagibin-ivan",
                            "name": "Nagibin Ivan",
                            "_links": {
                                "self": {
                                    "href": "/players/nagibin-ivan"
                                }
                            },
                            "number": 9
                        },
                        {
                            "id": "rylov-artur",
                            "name": "Rylov Artur",
                            "_links": {
                                "self": {
                                    "href": "/players/rylov-artur"
                                }
                            },
                            "number": 11
                        }
                    ]
                }
            }
        ],
        "season": {
            "name": "Division 1 2016/2017",
            "_links": {
                "self": {
                    "href": "/tournaments/rus_d1/seasons/20162017"
                }
            }
        },
        "stage": {
            "name": "Main",
            "_links": {
                "self": {
                    "href": "/tournaments/rus_d1/seasons/20162017/stages/main"
                }
            }
        },
        "_links": {
            "self": {
                "href": "/tournaments/rus_d1/seasons/20162017/stages/main/matches/51bcf895296312311248f8a728e6497e"
            }
        },
        "context": {
            "matchday": 22
        },
        "last_update_time": {
            "date_time": "2016-11-13T11:14:07+00:00",
            "timestamp": 1479035647
        }
    },
    {
        "id": "9e953578880cdeb398957a01d53e4268",
        "begin_time": {
            "date_time": "2016-11-13T11:00:00+00:00",
            "timestamp": 1479034800
        },
        "status": {
            "status": "scheduled",
            "score": [
                0,
                0
            ]
        },
        "tournament": {
            "id": "ukr_d2",
            "name": "Division 2",
            "_links": {
                "self": {
                    "href": "/tournaments/ukr_d2"
                }
            },
            "coverage": {
                "id": "ukr",
                "name": "Ukraine",
                "_links": {
                    "self": {
                        "href": "/territories/ukr"
                    }
                }
            }
        },
        "teams": [
            {
                "id": "fcpol_ukr",
                "name": "FC Poltava",
                "_links": {
                    "self": {
                        "href": "/teams/fcpol_ukr"
                    }
                }
            },
            {
                "id": "arskie_ukr",
                "name": "Arsenal Kiev",
                "_links": {
                    "self": {
                        "href": "/teams/arskie_ukr"
                    }
                }
            }
        ],
        "season": {
            "name": "Division 2 2016/2017",
            "_links": {
                "self": {
                    "href": "/tournaments/ukr_d2/seasons/20162017"
                }
            }
        },
        "stage": {
            "name": "Main",
            "_links": {
                "self": {
                    "href": "/tournaments/ukr_d2/seasons/20162017/stages/main"
                }
            }
        },
        "_links": {
            "self": {
                "href": "/tournaments/ukr_d2/seasons/20162017/stages/main/matches/9e953578880cdeb398957a01d53e4268"
            }
        },
        "context": {
            "matchday": "Round 19"
        },
        "last_update_time": {
            "date_time": "2016-11-13T00:00:06+00:00",
            "timestamp": 1478995206
        }
    },
    {
        "id": "dc007d56de13ed6180c102f3448e4683",
        "begin_time": {
            "date_time": "2016-11-13T11:00:00+00:00",
            "timestamp": 1479034800
        },
        "status": {
            "status": "online",
            "score": [
                0,
                0
            ],
            "period": "1T",
            "period_finish_time": {
                "date_time": "2016-11-13T11:44:47+00:00",
                "timestamp": 1479037487
            }
        },
        "tournament": {
            "id": "esp_sd",
            "name": "Segunda Division",
            "_links": {
                "self": {
                    "href": "/tournaments/esp_sd"
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
                "id": "lug_esp",
                "name": "Lugo",
                "_links": {
                    "self": {
                        "href": "/teams/lug_esp"
                    }
                },
                "squad": {
                    "eleven": [
                        {
                            "id": "pedraza-alfonso",
                            "name": "Pedraza Alfonso",
                            "_links": {
                                "self": {
                                    "href": "/players/pedraza-alfonso"
                                }
                            },
                            "number": 17
                        },
                        {
                            "id": "calavera-jordi",
                            "name": "Calavera Jordi",
                            "_links": {
                                "self": {
                                    "href": "/players/calavera-jordi"
                                }
                            },
                            "number": 23
                        },
                        {
                            "id": "campillo-antonio",
                            "name": "Campillo Antonio",
                            "_links": {
                                "self": {
                                    "href": "/players/campillo-antonio"
                                }
                            },
                            "number": 10
                        },
                        {
                            "id": "djalo-marcelo",
                            "name": "Djalo Marcelo",
                            "_links": {
                                "self": {
                                    "href": "/players/djalo-marcelo"
                                }
                            },
                            "number": 4
                        },
                        {
                            "id": "gonzalez-iriome",
                            "name": "Gonzalez Iriome",
                            "_links": {
                                "self": {
                                    "href": "/players/gonzalez-iriome"
                                }
                            },
                            "number": 24
                        },
                        {
                            "id": "joselu",
                            "name": "Joselu",
                            "_links": {
                                "self": {
                                    "href": "/players/joselu"
                                }
                            },
                            "number": 18
                        },
                        {
                            "id": "juan-jose",
                            "name": "Juan Jose",
                            "_links": {
                                "self": {
                                    "href": "/players/juan-jose"
                                }
                            },
                            "number": 1,
                            "role": "goalkeeper"
                        },
                        {
                            "id": "manu1",
                            "name": "Manu",
                            "_links": {
                                "self": {
                                    "href": "/players/manu1"
                                }
                            },
                            "number": 11
                        },
                        {
                            "id": "miquel-ignasi",
                            "name": "Miquel Ignasi",
                            "_links": {
                                "self": {
                                    "href": "/players/miquel-ignasi"
                                }
                            },
                            "number": 20
                        },
                        {
                            "id": "pita-carlos",
                            "name": "Pita Carlos",
                            "_links": {
                                "self": {
                                    "href": "/players/pita-carlos"
                                }
                            },
                            "number": 5
                        },
                        {
                            "id": "seoane-fernando",
                            "name": "Seoane Fernando",
                            "_links": {
                                "self": {
                                    "href": "/players/seoane-fernando"
                                }
                            },
                            "number": 8
                        }
                    ],
                    "substitutions": [
                        {
                            "id": "caballero-pablo",
                            "name": "Caballero Pablo",
                            "_links": {
                                "self": {
                                    "href": "/players/caballero-pablo"
                                }
                            },
                            "number": 9
                        },
                        {
                            "id": "fernandez-roberto",
                            "name": "Fernandez Roberto",
                            "_links": {
                                "self": {
                                    "href": "/players/fernandez-roberto"
                                }
                            },
                            "number": 13,
                            "role": "goalkeeper"
                        },
                        {
                            "id": "gil-sergio",
                            "name": "Gil Sergio",
                            "_links": {
                                "self": {
                                    "href": "/players/gil-sergio"
                                }
                            },
                            "number": 21
                        },
                        {
                            "id": "hernandez-carlos",
                            "name": "Hernandez Carlos",
                            "_links": {
                                "self": {
                                    "href": "/players/hernandez-carlos"
                                }
                            },
                            "number": 6
                        },
                        {
                            "id": "leuko-serge",
                            "name": "Leuko Serge",
                            "_links": {
                                "self": {
                                    "href": "/players/leuko-serge"
                                }
                            },
                            "number": 2
                        },
                        {
                            "id": "martinez-igor",
                            "name": "Martinez Igor",
                            "_links": {
                                "self": {
                                    "href": "/players/martinez-igor"
                                }
                            },
                            "number": 7
                        },
                        {
                            "id": "perea-brayan",
                            "name": "Perea Brayan",
                            "_links": {
                                "self": {
                                    "href": "/players/perea-brayan"
                                }
                            },
                            "number": 12
                        }
                    ]
                }
            },
            {
                "id": "rayval_esp",
                "name": "Rayo Vallecano",
                "_links": {
                    "self": {
                        "href": "/teams/rayval_esp"
                    }
                },
                "squad": {
                    "eleven": [
                        {
                            "id": "amaya-antonio",
                            "name": "Amaya Antonio",
                            "_links": {
                                "self": {
                                    "href": "/players/amaya-antonio"
                                }
                            },
                            "number": 4
                        },
                        {
                            "id": "cristaldo-franco",
                            "name": "Cristaldo Franco",
                            "_links": {
                                "self": {
                                    "href": "/players/cristaldo-franco"
                                }
                            },
                            "number": 16
                        },
                        {
                            "id": "galan-ernesto",
                            "name": "Galan Ernesto",
                            "_links": {
                                "self": {
                                    "href": "/players/galan-ernesto"
                                }
                            },
                            "number": 2
                        },
                        {
                            "id": "gazzaniga-paulo",
                            "name": "Gazzaniga Paulo",
                            "_links": {
                                "self": {
                                    "href": "/players/gazzaniga-paulo"
                                }
                            },
                            "number": 1,
                            "role": "goalkeeper"
                        },
                        {
                            "id": "manucho",
                            "name": "Manucho",
                            "_links": {
                                "self": {
                                    "href": "/players/manucho"
                                }
                            },
                            "number": 9
                        },
                        {
                            "id": "mojica-johan",
                            "name": "Mojica Johan",
                            "_links": {
                                "self": {
                                    "href": "/players/mojica-johan"
                                }
                            },
                            "number": 12
                        },
                        {
                            "id": "moreno-alex",
                            "name": "Moreno Alex",
                            "_links": {
                                "self": {
                                    "href": "/players/moreno-alex"
                                }
                            },
                            "number": 6
                        },
                        {
                            "id": "rat-razvan",
                            "name": "Rat Razvan",
                            "_links": {
                                "self": {
                                    "href": "/players/rat-razvan"
                                }
                            },
                            "number": 15
                        },
                        {
                            "id": "trashorras-roberto",
                            "name": "Trashorras Roberto",
                            "_links": {
                                "self": {
                                    "href": "/players/trashorras-roberto"
                                }
                            },
                            "number": 10
                        },
                        {
                            "id": "ze-castro",
                            "name": "Ze Castro",
                            "_links": {
                                "self": {
                                    "href": "/players/ze-castro"
                                }
                            },
                            "number": 18
                        },
                        {
                            "id": "zuculini-bruno",
                            "name": "Zuculini Bruno",
                            "_links": {
                                "self": {
                                    "href": "/players/zuculini-bruno"
                                }
                            },
                            "number": 25
                        }
                    ],
                    "substitutions": [
                        {
                            "id": "aguirre-diego",
                            "name": "Aguirre Diego",
                            "_links": {
                                "self": {
                                    "href": "/players/aguirre-diego"
                                }
                            },
                            "number": 22
                        },
                        {
                            "id": "claveria",
                            "name": "Claveria",
                            "_links": {
                                "self": {
                                    "href": "/players/claveria"
                                }
                            },
                            "number": 28
                        },
                        {
                            "id": "ebert-patrick",
                            "name": "Ebert Patrick",
                            "_links": {
                                "self": {
                                    "href": "/players/ebert-patrick"
                                }
                            },
                            "number": 20
                        },
                        {
                            "id": "miku",
                            "name": "Miku",
                            "_links": {
                                "self": {
                                    "href": "/players/miku"
                                }
                            },
                            "number": 7
                        },
                        {
                            "id": "garcia-luis",
                            "name": "Garcia Luis",
                            "_links": {
                                "self": {
                                    "href": "/players/garcia-luis"
                                }
                            },
                            "number": 30,
                            "role": "goalkeeper"
                        },
                        {
                            "id": "piti",
                            "name": "Piti",
                            "_links": {
                                "self": {
                                    "href": "/players/piti"
                                }
                            },
                            "number": 23
                        },
                        {
                            "id": "quini",
                            "name": "Quini",
                            "_links": {
                                "self": {
                                    "href": "/players/quini"
                                }
                            },
                            "number": 17
                        }
                    ]
                }
            }
        ],
        "season": {
            "name": "LaLiga2 2016/2017",
            "_links": {
                "self": {
                    "href": "/tournaments/esp_sd/seasons/20162017"
                }
            }
        },
        "stage": {
            "name": "Main",
            "_links": {
                "self": {
                    "href": "/tournaments/esp_sd/seasons/20162017/stages/main"
                }
            }
        },
        "_links": {
            "self": {
                "href": "/tournaments/esp_sd/seasons/20162017/stages/main/matches/dc007d56de13ed6180c102f3448e4683"
            }
        },
        "context": {
            "matchday": 14
        },
        "last_update_time": {
            "date_time": "2016-11-13T11:26:02+00:00",
            "timestamp": 1479036362
        },
        "events": [
            {
                "type": "goal",
                "team": {
                    "id": "lug_esp",
                    "name": "Lugo",
                    "_links": {
                        "self": {
                            "href": "/teams/lug_esp"
                        }
                    }
                },
                "moment": {
                    "period": "1T",
                    "moment": {
                        "minute": 25
                    }
                },
                "player": {
                    "id": "seoane-fernando",
                    "name": "Seoane Fernando",
                    "_links": {
                        "self": {
                            "href": "/players/seoane-fernando"
                        }
                    }
                },
                "score": [
                    1,
                    0
                ]
            }
        ]
    },
    {
        "id": "b8f32c20586568c9e9a0387968cb220f",
        "begin_time": {
            "date_time": "2016-11-13T11:30:00+00:00",
            "timestamp": 1479036600
        },
        "status": {
            "status": "scheduled",
            "score": [
                0,
                0
            ]
        },
        "tournament": {
            "id": "ita_sb",
            "name": "Serie B",
            "_links": {
                "self": {
                    "href": "/tournaments/ita_sb"
                }
            },
            "coverage": {
                "id": "ita",
                "name": "Italy",
                "_links": {
                    "self": {
                        "href": "/territories/ita"
                    }
                }
            }
        },
        "teams": [
            {
                "id": "ces_ita",
                "name": "Cesena",
                "_links": {
                    "self": {
                        "href": "/teams/ces_ita"
                    }
                },
                "squad": {
                    "eleven": [
                        {
                            "id": "agliardi-federico",
                            "name": "Agliardi Federico",
                            "_links": {
                                "self": {
                                    "href": "/players/agliardi-federico"
                                }
                            },
                            "number": 1,
                            "role": "goalkeeper"
                        },
                        {
                            "id": "balzano-antonio",
                            "name": "Balzano Antonio",
                            "_links": {
                                "self": {
                                    "href": "/players/balzano-antonio"
                                }
                            },
                            "number": 14
                        },
                        {
                            "id": "capelli-daniele",
                            "name": "Capelli Daniele",
                            "_links": {
                                "self": {
                                    "href": "/players/capelli-daniele"
                                }
                            },
                            "number": 25
                        },
                        {
                            "id": "cascione-emmanuel",
                            "name": "Cascione Emmanuel",
                            "_links": {
                                "self": {
                                    "href": "/players/cascione-emmanuel"
                                }
                            },
                            "number": 4
                        },
                        {
                            "id": "ciano-camillo",
                            "name": "Ciano Camillo",
                            "_links": {
                                "self": {
                                    "href": "/players/ciano-camillo"
                                }
                            },
                            "number": 10
                        },
                        {
                            "id": "cinelli-antonio",
                            "name": "Cinelli Antonio",
                            "_links": {
                                "self": {
                                    "href": "/players/cinelli-antonio"
                                }
                            },
                            "number": 6
                        },
                        {
                            "id": "dalmonte-nicola",
                            "name": "Dalmonte Nicola",
                            "_links": {
                                "self": {
                                    "href": "/players/dalmonte-nicola"
                                }
                            },
                            "number": 26
                        },
                        {
                            "id": "falasco-nicola",
                            "name": "Falasco Nicola",
                            "_links": {
                                "self": {
                                    "href": "/players/falasco-nicola"
                                }
                            },
                            "number": 20
                        },
                        {
                            "id": "kone-moussa",
                            "name": "Kone Moussa",
                            "_links": {
                                "self": {
                                    "href": "/players/kone-moussa"
                                }
                            },
                            "number": 23
                        },
                        {
                            "id": "ligi-alessandro",
                            "name": "Ligi Alessandro",
                            "_links": {
                                "self": {
                                    "href": "/players/ligi-alessandro"
                                }
                            },
                            "number": 27
                        },
                        {
                            "id": "rodriguez-alejandro",
                            "name": "Rodriguez Alejandro",
                            "_links": {
                                "self": {
                                    "href": "/players/rodriguez-alejandro"
                                }
                            },
                            "number": 9
                        }
                    ],
                    "substitutions": [
                        {
                            "id": "bardini-lorenzo",
                            "name": "Bardini Lorenzo",
                            "_links": {
                                "self": {
                                    "href": "/players/bardini-lorenzo"
                                }
                            },
                            "number": 32,
                            "role": "goalkeeper"
                        },
                        {
                            "id": "di-roberto-nunzio",
                            "name": "Di Roberto Nunzio",
                            "_links": {
                                "self": {
                                    "href": "/players/di-roberto-nunzio"
                                }
                            },
                            "number": 34
                        },
                        {
                            "id": "panico-giuseppe",
                            "name": "Panico Giuseppe",
                            "_links": {
                                "self": {
                                    "href": "/players/panico-giuseppe"
                                }
                            },
                            "number": 17
                        },
                        {
                            "id": "renzetti-francesco",
                            "name": "Renzetti Francesco",
                            "_links": {
                                "self": {
                                    "href": "/players/renzetti-francesco"
                                }
                            },
                            "number": 33
                        },
                        {
                            "id": "rigione-michele",
                            "name": "Rigione Michele",
                            "_links": {
                                "self": {
                                    "href": "/players/rigione-michele"
                                }
                            },
                            "number": 16
                        },
                        {
                            "id": "wolski-bartosz",
                            "name": "Wolski Bartosz",
                            "_links": {
                                "self": {
                                    "href": "/players/wolski-bartosz"
                                }
                            },
                            "number": 35
                        }
                    ]
                }
            },
            {
                "id": "pis_ita",
                "name": "Pisa",
                "_links": {
                    "self": {
                        "href": "/teams/pis_ita"
                    }
                },
                "squad": {
                    "eleven": [
                        {
                            "id": "cardelli-daniele",
                            "name": "Cardelli Daniele",
                            "_links": {
                                "self": {
                                    "href": "/players/cardelli-daniele"
                                }
                            },
                            "number": 22,
                            "role": "goalkeeper"
                        },
                        {
                            "id": "crescenzi-luca",
                            "name": "Crescenzi Luca",
                            "_links": {
                                "self": {
                                    "href": "/players/crescenzi-luca"
                                }
                            },
                            "number": 13
                        },
                        {
                            "id": "di-tacchio-francesco",
                            "name": "Di Tacchio Francesco",
                            "_links": {
                                "self": {
                                    "href": "/players/di-tacchio-francesco"
                                }
                            },
                            "number": 6
                        },
                        {
                            "id": "eusepi-umberto",
                            "name": "Eusepi Umberto",
                            "_links": {
                                "self": {
                                    "href": "/players/eusepi-umberto"
                                }
                            },
                            "number": 23
                        },
                        {
                            "id": "golubovic-petar",
                            "name": "Golubovic Petar",
                            "_links": {
                                "self": {
                                    "href": "/players/golubovic-petar"
                                }
                            },
                            "number": 24
                        },
                        {
                            "id": "lisuzzo-andrea",
                            "name": "Lisuzzo Andrea",
                            "_links": {
                                "self": {
                                    "href": "/players/lisuzzo-andrea"
                                }
                            },
                            "number": 4
                        },
                        {
                            "id": "longhi-alessandro",
                            "name": "Longhi Alessandro",
                            "_links": {
                                "self": {
                                    "href": "/players/longhi-alessandro"
                                }
                            },
                            "number": 3
                        },
                        {
                            "id": "lores-ignacio",
                            "name": "Lores Ignacio",
                            "_links": {
                                "self": {
                                    "href": "/players/lores-ignacio"
                                }
                            },
                            "number": 10
                        },
                        {
                            "id": "peralta-diego",
                            "name": "Peralta Diego",
                            "_links": {
                                "self": {
                                    "href": "/players/peralta-diego"
                                }
                            },
                            "number": 20
                        },
                        {
                            "id": "sanseverino-giulio",
                            "name": "Sanseverino Giulio",
                            "_links": {
                                "self": {
                                    "href": "/players/sanseverino-giulio"
                                }
                            },
                            "number": 27
                        },
                        {
                            "id": "verna-luca",
                            "name": "Verna Luca",
                            "_links": {
                                "self": {
                                    "href": "/players/verna-luca"
                                }
                            },
                            "number": 8
                        }
                    ],
                    "substitutions": [
                        {
                            "id": "d-angina-ramon",
                            "name": "D Angina Ramon",
                            "_links": {
                                "self": {
                                    "href": "/players/d-angina-ramon"
                                }
                            },
                            "number": 31
                        },
                        {
                            "id": "fautario-simone",
                            "name": "Fautario Simone",
                            "_links": {
                                "self": {
                                    "href": "/players/fautario-simone"
                                }
                            },
                            "number": 30
                        },
                        {
                            "id": "favale-giulio",
                            "name": "Favale Giulio",
                            "_links": {
                                "self": {
                                    "href": "/players/favale-giulio"
                                }
                            },
                            "number": 26
                        },
                        {
                            "id": "gatto-massimiliano",
                            "name": "Gatto Massimiliano",
                            "_links": {
                                "self": {
                                    "href": "/players/gatto-massimiliano"
                                }
                            },
                            "number": 28
                        },
                        {
                            "id": "lazzari-andrea",
                            "name": "Lazzari Andrea",
                            "_links": {
                                "self": {
                                    "href": "/players/lazzari-andrea"
                                }
                            },
                            "number": 19
                        },
                        {
                            "id": "mudingayi-gaby",
                            "name": "Mudingayi Gaby",
                            "_links": {
                                "self": {
                                    "href": "/players/mudingayi-gaby"
                                }
                            },
                            "number": 35
                        }
                    ]
                }
            }
        ],
        "season": {
            "name": "Serie B 2016/2017",
            "_links": {
                "self": {
                    "href": "/tournaments/ita_sb/seasons/20162017"
                }
            }
        },
        "stage": {
            "name": "Main",
            "_links": {
                "self": {
                    "href": "/tournaments/ita_sb/seasons/20162017/stages/main"
                }
            }
        },
        "_links": {
            "self": {
                "href": "/tournaments/ita_sb/seasons/20162017/stages/main/matches/b8f32c20586568c9e9a0387968cb220f"
            }
        },
        "context": {
            "matchday": 14
        },
        "last_update_time": {
            "date_time": "2016-11-13T11:20:02+00:00",
            "timestamp": 1479036002
        }
    }
]
```