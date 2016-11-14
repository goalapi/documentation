# Matches
This describes API-calls to fetch data about Tournaments current Subscription has access to  

1. [List all Tournaments available for current API-key](#list-matches-from-particular-season-or-stage)
1. [Get Tournament by ID](#get-tournament-by-id)
1. [Tournament properties explained](#get-tournament-by-id)
1. [Get Matches and other data from Tournament](#list-online-matches)

## List all Tournaments available for current API-key

```
GET /v1/tournaments/
```

This API-call returns array of Tournament items.   

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
    