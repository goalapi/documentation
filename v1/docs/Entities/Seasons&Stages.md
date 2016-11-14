# Seasons and Stages
This describes API-calls to fetch Matches

1. [List Tournament's Seasons](#list-matches-from-particular-season-or-stage)
1. [Get Season by ID](#get-match-by-id)
1. [List Season's Stages](#list-online-matches)
1. [Get Stage by ID](Match/properties.md#match-properties-explained)
1. [Get Standings from Stage](Match/properties.md#match-properties-explained)
1. [List Matches from Season or Stage]
1. [List Teams from Season or Stage]


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

Seasons and Stages do not have explicit IDs. For identification purposes clients may use value of `_links.self.href` attribute.   