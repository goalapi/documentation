
## Match properties explained  

This will explain meaning and usage of Match properties     

1. [Begin time](#begin-time) 
1. [Match status](#match-status) 
1. [Current minute of live Match](#current-minute-of-live-match) 
1. [Teams](#teams) 
1. [Teams Lineups](#teams-lineups) 
1. [Match Context](#match-context) 
1. [Match Events](#match-events) 
1. [Penalty Shootout](#penalty-shootout) 


### Begin Time
This property represents time moment where Match is supposed to start or already started. Representation of all Date-Time objects is an object with `date_time` and `timestamp`. 
 
 **Example:**
 ```json
 {
    "begin_time": {
        "date_time": "2016-09-25T15:00:00+00:00",
        "timestamp": 1474815600
    }
 }
 ```
 
 - `date-time` field is [ISO 8601](https://www.w3.org/TR/NOTE-datetime) representation of Date-Time
 - `timestamp` is a number of seconds gone from **1970-01-01T00:00:00+00:00**
 
### Match status 
 The `status` property contains data about current state of Match. 
 
 **Example:**
 ```json 
    {
         "status": {
             "status": "online",
             "score": [
                 0,
                 0
             ],
             "period_finish_time": {
                 "date_time": "2016-09-25T15:00:00+00:00",
                 "timestamp": 1474815600
             }
         }
    }
 ```
Depending on state of Match, `status` field it may have different set of properties:
 
 - `status` - indicates the state of Match, can be _online_, _scheduled_, _finished_, _postponed_, _interrupted_, _canceled_;
 - `score` - the array containing the score of Match; zero-indexed item is a score of hosts team, next item is score of visitors team;
 - `period` - current period of _online_ Matches; 
    - `1T`, `2T` - first and second halves of basic time    
    - `HT` - half-time break
    - `ET`, `E1T`,  `E2T` - extra-time of match or first or second half of extra-time (if possible)  
    - `EHT` - break between two halves of extra-time
    - `PS` - penalty shootout
 - `period_finish_time` - if Match is online, indicates the moment when current period supposed to be finished; 
    since we know the duration length of each period, it allows to determine current minute;
 - `finished_after` - indicates the last period of finished Match
 - `reason` - contains description of reason of abnormal flow for _postponed_, _canceled_ and _interrupted_ Matches

### Current minute of live Match
 Current minute is not provided explicitly as a property of live Match object. API consumers are offered to calculate
it on their end using `period_finish_time` field of Match `status`. 
The simple formula for current minute calculation is as follows:
```
   current_minute_of_match = last_minute_of_current_period - Math.floor((period_finish_timestamp - current_timestamp)/60)
``` 
where `current_timestamp` is a [Unix Timestamp](https://en.wikipedia.org/wiki/Unix_time) of current moment,
`period_finish_timestamp` is a Unix Timestamp of moment when current period is supposed to finish,
`Math.floor` - is something like [JavaScript Math.floor](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/floor) 
function,
`last_minute_of_current_period` - is a number indicating final minute for current period; it's different for each period of Match:
   - 45 for `1T`
   - 90 for `2T`
   - 105 for `E1T`
   - 120 for `ET` and `E2T`
   
The minute must not be calculated for all other periods of Match

   
### Teams

 This field is an array containing info about Teams taking part in this Match. 
 Zero-indexed item is a hosts Team, next item is a visitors Team.

 **Example:**
 ```json
    {
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
        ]
    } 
 ```

### Teams Lineups
 In the cases when Match object contains full representation, it must contain info about teams lineups . 
 Lineups added as additional `squad` field to each team in `Teams` field. `Squad` fields have 2 fields: `elntn` - array of 
 players which starts the match on pitch and `substitutions` - array of substitution players.  

 **Example:**
 ```json
    {
        "teams": [
            {
                "id": "wesham_eng",
                "name": "West Ham",
                "_links": {
                    "self": {
                        "href": "/teams/wesham_eng"
                    }
                },
                "squad": {
                    "eleven": [],
                    "substitutions": []
                }
            },
            {
                "id": "sou_eng",
                "name": "Southampton",
                "_links": {
                    "self": {
                        "href": "/teams/sou_eng"
                    }
                },
                "squad": {
                    "eleven": [],
                    "substitutions": []
                }            
            }
        ]
    }
 ```
 
 Each item of `eleven` and `substitutions` arrays is an object containing info about player and his position on pitch.   
  **Example:**
  ```json
    {
        "teams": [
            {
                "id": "wesham_eng",
                "name": "West Ham",
                "_links": {
                    "self": {
                        "href": "/teams/wesham_eng"
                    }
                },
                "squad": {
                    "eleven": [
                        {
                            "id": "nyom-allan",
                            "name": "Nyom Allan",
                            "_links": {
                                "self": {
                                    "href": "/players/nyom-allan"
                                }
                            },
                            "number": 2
                        }, {
                            "id": "pantilimon-costel",
                            "name": "Pantilimon Costel",
                            "_links": {
                                "self": {
                                    "href": "/players/pantilimon-costel"
                                }
                            },
                            "number": 30,
                            "role": "goalkeeper"
                        }                    
                    ]
                }
            }
        ]
    }
  ```

### Match Context
 The `context` field contains some Match attributes linking it to different competition parts, which competition divided to inside the Stage. 
 It can be `group` for group stage or `zone` for competitions with geographical conferences and anything else.  
 
 **Example:**
 ```json
 {
    "id": "07ca0d9c08b31c9a1783cee266836a25",
    "begin_time": {
        "date_time": "2016-08-13T11:30:00+00:00",
        "timestamp": 1471087800
    },
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
    "context": {
         "matchday": "Round 1"
    }
 }
 
 ```
 
### Match Events
 The `events` field contains array of `Event` objects. Each `Event` can have following fields: 
  - `type` - the type of event; following types are possible:
    - `goal`
    - `card`
    - `substituion`
    - `penalty_missed`
    
  - `team` - the Team which player(s) caused this event
  - `moment` - moment of Match when event happened
  - `player` - Player caused this Event
  - `players` - two players for Substitution event    
  - `color` - card type for yellow or red card events; card color can be 
      - `yellow`
      - `red`
      - `yellow_red`

 **Example:**
 ```json
 {
    "events": [
        {
            "type": "card",
            "team": {
                "id": "lei_eng",
                "name": "Leicester",
                "_links": {
                    "self": {
                        "href": "/teams/lei_eng"
                    }
                }
            },
            "moment": {
                "period": "1T",
                "minute": 29
            },
            "color": "yellow",
            "player": {
                "id": "fuchs-christian",
                "name": "Fuchs Christian",
                "_links": {
                    "self": {
                        "href": "/players/fuchs-christian"
                    }
                }
            }
        },
        {
            "type": "card",
            "team": {
                "id": "lei_eng",
                "name": "Leicester",
                "_links": {
                    "self": {
                        "href": "/teams/lei_eng"
                    }
                }
            },
            "moment": {
                "period": "1T",
                "minute": 33
            },
            "color": "yellow",
            "player": {
                "id": "simpson-danny",
                "name": "Simpson Danny",
                "_links": {
                    "self": {
                        "href": "/players/simpson-danny"
                    }
                }
            }
        },
        {
            "type": "goal",
            "team": {
                "id": "hulcit_eng",
                "name": "Hull City",
                "_links": {
                    "self": {
                        "href": "/teams/hulcit_eng"
                    }
                }
            },
            "moment": {
                "period": "1T",
                "minute": 46
            },
            "player": {
                "id": "diomande-adama",
                "name": "Diomande Adama",
                "_links": {
                    "self": {
                        "href": "/players/diomande-adama"
                    }
                }
            },
            "score": [
                1,
                0
            ]
        },
        {
            "type": "goal",
            "team": {
                "id": "lei_eng",
                "name": "Leicester",
                "_links": {
                    "self": {
                        "href": "/teams/lei_eng"
                    }
                }
            },
            "moment": {
                "period": "2T",
                "minute": 47
            },
            "player": {
                "id": "mahrez-riyad",
                "name": "Mahrez Riyad",
                "_links": {
                    "self": {
                        "href": "/players/mahrez-riyad"
                    }
                }
            },
            "score": [
                1,
                1
            ]
        },
        {
            "type": "goal",
            "team": {
                "id": "hulcit_eng",
                "name": "Hull City",
                "_links": {
                    "self": {
                        "href": "/teams/hulcit_eng"
                    }
                }
            },
            "moment": {
                "period": "2T",
                "minute": 57
            },
            "player": {
                "id": "snodgrass-robert",
                "name": "Snodgrass Robert",
                "_links": {
                    "self": {
                        "href": "/players/snodgrass-robert"
                    }
                }
            },
            "score": [
                2,
                1
            ]
        },
        {
            "type": "substitution",
            "team": {
                "id": "lei_eng",
                "name": "Leicester",
                "_links": {
                    "self": {
                        "href": "/teams/lei_eng"
                    }
                }
            },
            "moment": {
                "period": "2T",
                "minute": 68
            },
            "players": {
                "in": {
                    "id": "okazaki-shinji",
                    "name": "Okazaki Shinji",
                    "_links": {
                        "self": {
                            "href": "/players/okazaki-shinji"
                        }
                    }
                },
                "out": {
                    "id": "gray-demarai",
                    "name": "Gray Demarai",
                    "_links": {
                        "self": {
                            "href": "/players/gray-demarai"
                        }
                    }
                }
            }
        },
        {
            "type": "substitution",
            "team": {
                "id": "lei_eng",
                "name": "Leicester",
                "_links": {
                    "self": {
                        "href": "/teams/lei_eng"
                    }
                }
            },
            "moment": {
                "period": "2T",
                "minute": 68
            },
            "players": {
                "in": {
                    "id": "amartey-daniel",
                    "name": "Amartey Daniel",
                    "_links": {
                        "self": {
                            "href": "/players/amartey-daniel"
                        }
                    }
                },
                "out": {
                    "id": "king-andy",
                    "name": "King Andy",
                    "_links": {
                        "self": {
                            "href": "/players/king-andy"
                        }
                    }
                }
            }
        }
    ]    
 }
 ```

### Penalty Shootout

Matches with penalty shootout series will have additional attribute `penalty_shootout` which stores an object with tow fields: `score` and `kicks`. 
 - `score` - is score of penalty shootout
 - `kicks` - is an array of items representing info about each kick; if kick is missed - it will have additional attribute `"missed": true` 

**Example:**

```json
{
"penalty_shootout": {
        "score": [
            3,
            2
        ],
        "kicks": [
            {
                "team": {
                    "id": "bra_nat",
                    "name": "Brazil",
                    "_links": {
                        "self": {
                            "href": "/teams/bra_nat"
                        }
                    }
                },
                "player": {
                    "id": "luiz-david",
                    "name": "Luiz David",
                    "_links": {
                        "self": {
                            "href": "/players/luiz-david"
                        }
                    }
                },
                "score": [
                    1,
                    0
                ]
            },
            {
                "team": {
                    "id": "chl_nat",
                    "name": "Chile",
                    "_links": {
                        "self": {
                            "href": "/teams/chl_nat"
                        }
                    }
                },
                "missed": true,
                "player": {
                    "id": "pinilla-mauricio",
                    "name": "Pinilla Mauricio",
                    "_links": {
                        "self": {
                            "href": "/players/pinilla-mauricio"
                        }
                    }
                }
            },
            {
                "team": {
                    "id": "bra_nat",
                    "name": "Brazil",
                    "_links": {
                        "self": {
                            "href": "/teams/bra_nat"
                        }
                    }
                },
                "missed": true,
                "player": {
                    "id": "willian",
                    "name": "Willian",
                    "_links": {
                        "self": {
                            "href": "/players/willian"
                        }
                    }
                }
            },
            {
                "team": {
                    "id": "chl_nat",
                    "name": "Chile",
                    "_links": {
                        "self": {
                            "href": "/teams/chl_nat"
                        }
                    }
                },
                "missed": true,
                "player": {
                    "id": "sanchez-alexis",
                    "name": "Sanchez Alexis",
                    "_links": {
                        "self": {
                            "href": "/players/sanchez-alexis"
                        }
                    }
                }
            },
            {
                "team": {
                    "id": "bra_nat",
                    "name": "Brazil",
                    "_links": {
                        "self": {
                            "href": "/teams/bra_nat"
                        }
                    }
                },
                "player": {
                    "id": "marcelo",
                    "name": "Marcelo",
                    "_links": {
                        "self": {
                            "href": "/players/marcelo"
                        }
                    }
                },
                "score": [
                    2,
                    0
                ]
            },
            {
                "team": {
                    "id": "chl_nat",
                    "name": "Chile",
                    "_links": {
                        "self": {
                            "href": "/teams/chl_nat"
                        }
                    }
                },
                "player": {
                    "id": "aranguiz-charles",
                    "name": "Aranguiz Charles",
                    "_links": {
                        "self": {
                            "href": "/players/aranguiz-charles"
                        }
                    }
                },
                "score": [
                    2,
                    1
                ]
            },
            {
                "team": {
                    "id": "bra_nat",
                    "name": "Brazil",
                    "_links": {
                        "self": {
                            "href": "/teams/bra_nat"
                        }
                    }
                },
                "missed": true,
                "player": {
                    "id": "hulk",
                    "name": "Hulk",
                    "_links": {
                        "self": {
                            "href": "/players/hulk"
                        }
                    }
                }
            },
            {
                "team": {
                    "id": "chl_nat",
                    "name": "Chile",
                    "_links": {
                        "self": {
                            "href": "/teams/chl_nat"
                        }
                    }
                },
                "player": {
                    "id": "diaz-marcelo",
                    "name": "Diaz Marcelo",
                    "_links": {
                        "self": {
                            "href": "/players/diaz-marcelo"
                        }
                    }
                },
                "score": [
                    2,
                    2
                ]
            },
            {
                "team": {
                    "id": "bra_nat",
                    "name": "Brazil",
                    "_links": {
                        "self": {
                            "href": "/teams/bra_nat"
                        }
                    }
                },
                "player": {
                    "id": "neymar",
                    "name": "Neymar",
                    "_links": {
                        "self": {
                            "href": "/players/neymar"
                        }
                    }
                },
                "score": [
                    3,
                    2
                ]
            },
            {
                "team": {
                    "id": "chl_nat",
                    "name": "Chile",
                    "_links": {
                        "self": {
                            "href": "/teams/chl_nat"
                        }
                    }
                },
                "missed": true,
                "player": {
                    "id": "jara-gonzalo",
                    "name": "Jara Gonzalo",
                    "_links": {
                        "self": {
                            "href": "/players/jara-gonzalo"
                        }
                    }
                }
            }
        ]
    }
}
```