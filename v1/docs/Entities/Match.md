## List Matches from particular Season or Stage

```
GET /tournaments/:tournamentId/seasons/:seasonId/matches/:page/
GET /tournaments/:tournamentId/seasons/:seasonId/stages/:stageId/matches/:page/
```

Lists all matches from Season or Stage specified in path. These API-calls returns array of items, each item represents summary of Match. Summaries DO NOT include info about Teams Lineups and Match Events (like goals, cards, etc...).

### Example
```
$ curl http://api.goalapi.com/v1/tournaments/eng_pl/seasons/20162017/matches/1/

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