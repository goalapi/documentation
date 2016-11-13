# Matches
This describes API-calls to fetch Matches

1. [List Matches from particular Season or Stage](#list-matches-from-particular-season-or-stage)
1. [Get Match by ID](#get-match-by-id)
1. [List online Matches](#list-online-matches)
1. [Match properties explained](Match/properties.md#match-properties-explained)

## List Matches from particular Season or Stage

```
GET /v1/tournaments/:tournamentId/seasons/:seasonId/matches/:page/
GET /v1/tournaments/:tournamentId/seasons/:seasonId/stages/:stageId/matches/:page/
```

Lists all matches from Season or Stage specified in path. These API-calls returns array of items, each item represents summary of Match. Summaries DO NOT include info about Teams Lineups and Match Events (like goals, cards, etc...).

### Example
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

## Get Match by ID

```
GET /tournaments/:tournamentId/seasons/:seasonId/matches/:matchId
GET /tournaments/:tournamentId/seasons/:seasonId/stages/:stageId/matches/:matchId
```

Returns one Match by **matchId** from Season or Stage specified in path. These API-calls return one Match with full details i.e with Events and Team lineups if available.  

### Example
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
