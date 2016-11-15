# Date-Time object
This property represents time moment where Match is supposed to start or already started. 
Representation of all Date-Time objects is an object with `date_time` and `timestamp`.

## Properties
 
* `date-time` - String -  [ISO 8601](https://www.w3.org/TR/NOTE-datetime) representation of Date-Time
* `timestamp` - Number - number of seconds gone from _1970-01-01T00:00:00+00:00_

**Example:**
 ```json
 {
    "date_time": "2016-09-25T15:00:00+00:00",
    "timestamp": 1474815600
 }
 ```
