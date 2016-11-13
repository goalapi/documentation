
## Match properties explained  

This will explain meaning and usage of Match properties     

1. [Begin time](#begin-time) 
1. [Match status](#match-status) 
1. [Teams](#teams) 
1. [Teams Lineups](#teams-lineups) 


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
 Lineups added as additional `squad` field to each team in `field`. `Squad` fields have 2 fields: `eleven` - array of 
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
  