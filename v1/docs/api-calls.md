
#API-calls reference 

API-calls is another name for requests which clients made to our API via HTTP

## List of API-calls
* [/](#root)
* [/tournaments/](#tournaments)
* [/tournaments/:tournamentId](#tournament)
* [/tournaments/:tournamentId/seasons/](#seasons)
* [/tournaments/:tournamentId/seasons/:seasonId](#season)
* [/tournaments/:tournamentId/seasons/:seasonId/teams/](#season-teams)
* [/tournaments/:tournamentId/seasons/:seasonId/teams/:teamId](#season-team)
* [/tournaments/:tournamentId/seasons/:seasonId/matches/](#season-matches)
* [/tournaments/:tournamentId/seasons/:seasonId/matches/:matchId](#season-match)
* [/tournaments/:tournamentId/seasons/:seasonId/stages/](#stages)
* [/tournaments/:tournamentId/seasons/:seasonId/stages/:stageId](#stage)
* [/tournaments/:tournamentId/seasons/:seasonId/stages/:stageId/teams/](#stage-teams)
* [/tournaments/:tournamentId/seasons/:seasonId/stages/:stageId/teams/:teamId](#stage-team)
* [/tournaments/:tournamentId/seasons/:seasonId/stages/:stageId/matches/](#stage-matches)
* [/tournaments/:tournamentId/seasons/:seasonId/stages/:stageId/matches/:matchId](#stage-match)
* [/tournaments/:tournamentId/seasons/:seasonId/stages/:stageId/standings/](#stage-standings)
* [/teams/:teamId](#team)
* [/players/:playerId](#player)
* [/territories/:territoryId](#territory) 
* [/updates/](#updates)
* [/updates/:dataType/](#updates-by-data-types)


## Root 
```
    GET /
```
**Description:** Returns the current state of Subscription bound with API KEY

**Input parameters:** None

**Output:** [Subscription object](./definitions/Subscription.md)

**Read more:** [API Root Endpoint](../../README.md#root-endpoint)


## Tournaments
```
    GET /tournaments/
```
**Description:** Returns the list of all Tournaments available for current Subscription

**Input parameters:** None

**Output:** Array of [Tournament objects](./definitions/Tournament.md#brief)

**Read more:** [How to list all Tournaments available for client](./howto/Tournament.md#list-all-tournaments-available-for-current-api-key)


## Tournament
```
    GET /tournaments/:tournamentId
```
**Description:** Returns Tournament

**Input parameters:** 

   - `tournamentId` -  ID of Tournament (required)
      
**Output:** [Tournament object](./definitions/Tournament.md#full)

**Read more:** [How to get Tournament by ID](./howto/Tournament.md#get-tournament-by-id)


## Seasons 
```
    GET /tournaments/:tournamentId/seasons/
```
**Description:** Returns array of Seasons belonging to specified Tournament

**Input parameters:** 

   - `tournamentId` -  ID of Tournament (required)
      
**Output:** Array of [Season objects](./definitions/Season.md#brief)

**Read more:** [How to list all Seasons from Tournament](./howto/Seasons&Stages.md#list-tournaments-seasons)


## Season
```
    GET /tournaments/:tournamentId/seasons/:seasonId
```
**Description:** Returns the Season

**Input parameters:** 

   - `tournamentId` -  ID of Tournament (required)
   - `seasonId` -  ID of Season (required)
      
**Output:** [Season object](./definitions/Season.md#full)

**Read more:** [How to get Season by ID](./howto/Seasons&Stages.md#get-season-by-id)


## Season Teams
```
    GET /tournaments/:tournamentId/seasons/:seasonId/teams/
```
**Description:** Returns list of Teams taking part in specified Season

**Input parameters:** 

   - `tournamentId` -  ID of Tournament (required)
   - `seasonId` -  ID of Season (required)
      
**Output:** Array of [Squad objects](./definitions/Squad.md#brief)

**Read more:** [How to list all Teams in Season](./howto/Seasons&Stages.md#teams)


## Season Team
```
    GET /tournaments/:tournamentId/seasons/:seasonId/teams/:teamId
```
**Description:** Returns the Team details related to specified Season

**Input parameters:** 

   - `tournamentId` -  ID of Tournament (required)
   - `seasonId` -  ID of Season (required)
   - `teamId` -  ID of Team (required)
      
**Output:** [Squad object](./definitions/Squad.md#full)

**Read more:** [How to get Team's Line Ups for Season](./howto/Seasons&Stages.md#teams-line-ups-for-season-or-stage)


## Season Matches
```
    GET /tournaments/:tournamentId/seasons/:seasonId/matches/:page/
```
**Description:** Returns all Matches from specified Season

**Input parameters:** 

   - `tournamentId` -  ID of Tournament (required)
   - `seasonId` -  ID of Season (required)
   - `page` -  page number 
      
**Output:** Array of [Match objects](./definitions/Match.md#brief)

**Read more:** [How to list all Matches from Season](./howto/Seasons&Stages.md#matches)


## Season Match
```
    GET /tournaments/:tournamentId/seasons/:seasonId/matches/:matchId
```
**Description:** Returns full details of particular Match

**Input parameters:** 

   - `tournamentId` -  ID of Tournament (required)
   - `seasonId` -  ID of Season (required)
   - `matchId` -  ID of Match (required) 
      
**Output:** [Match object](./definitions/Match.md#full)

**Read more:** [How to get Match by ID](./howto/Seasons&Stages.md#get-match-by-id)


## Stages
```
    GET /tournaments/:tournamentId/seasons/:seasonId/stages/
```
**Description:** Returns the array of Stages belonging to specified Season

**Input parameters:** 

   - `tournamentId` -  ID of Tournament (required)
   - `seasonId` -  ID of Season (required)
      
**Output:** Array of [Stage objects](./definitions/Stage.md#brief)

**Read more:** [How to list all Stages in Season](./howto/Seasons&Stages.md#list-seasons-stages)


## Stage
```
    GET /tournaments/:tournamentId/seasons/:seasonId/stages/:stageId
```
**Description:** Returns specified Stage

**Input parameters:** 

   - `tournamentId` -  ID of Tournament (required)
   - `seasonId` -  ID of Season (required)
   - `stageId` -  ID of Stage (required)
      
**Output:** [Stage object](./definitions/Stage.md#full)

**Read more:** [How to get Stage by ID](./howto/Seasons&Stages.md#get-stage-by-id)


## Stage Teams
```
    GET /tournaments/:tournamentId/seasons/:seasonId/stages/:stageId/teams/
```
**Description:** Returns list of Teams taking part in specified Stage

**Input parameters:** 

   - `tournamentId` -  ID of Tournament (required)
   - `seasonId` -  ID of Season (required)
   - `stageId` -  ID of Stage (required)
      
**Output:** Array of [Squad objects](./definitions/Squad.md#brief)

**Read more:** [How to list all Teams in Stage](./howto/Seasons&Stages.md#teams)


## Stage Team
```
    GET /tournaments/:tournamentId/seasons/:seasonId/stages/:stageId/teams/:teamId
```
**Description:** Returns the Team details related to specified Stage

**Input parameters:** 

   - `tournamentId` -  ID of Tournament (required)
   - `seasonId` -  ID of Season (required)
   - `stageId` -  ID of Stage (required)
   - `teamId` -  ID of Team (required)
      
**Output:** [Squad object](./definitions/Squad.md#full)

**Read more:** [How to get Team's Line Ups for Stage](./howto/Seasons&Stages.md#teams-line-ups-for-season-or-stage)


## Stage Matches
```
    GET /tournaments/:tournamentId/seasons/:seasonId/stages/:stageId/matches/:page/
```
**Description:** Returns all Matches from specified Stage

**Input parameters:** 

   - `tournamentId` -  ID of Tournament (required)
   - `seasonId` -  ID of Season (required)
   - `stageId` -  ID of Stage (required)
   - `page` -  page number 
      
**Output:** Array of [Match objects](./definitions/Match.md#brief)

**Read more:** [How to list all Matches from Stage](./howto/Seasons&Stages.md#matches)


## Stage Match
```
    GET /tournaments/:tournamentId/seasons/:seasonId/stages/:stageId/matches/:matchId
```
**Description:** Returns full details of particular Match

**Input parameters:** 

   - `tournamentId` -  ID of Tournament (required)
   - `seasonId` -  ID of Season (required)
   - `stageId` -  ID of Stage (required)
   - `matchId` -  ID of Match (required) 
      
**Output:** [Match object](./definitions/Match.md#full)

**Read more:** [How to get Match by ID](./howto/Seasons&Stages.md#get-match-by-id)


## Stage Standings
```
    GET /tournaments/:tournamentId/seasons/:seasonId/stages/:stageId/standings/
```
**Description:** Returns Standings Tables if they exist for specified Stage

**Input parameters:** 

   - `tournamentId` -  ID of Tournament (required)
   - `seasonId` -  ID of Season (required)
   - `stageId` -  ID of Stage (required)
      
**Output:** Array of [StandingsTable objects](./definitions/StandingsTable.md)

**Read more:** [How to get Standings](./howto/Seasons&Stages.md#how-to-get-standings)


## Team
```
    GET /teams/:teamId
```
**Description:** Returns info about Team

**Input parameters:** 

   - `teamId` -  ID of Team (required)
      
**Output:** [Team object](./definitions/Team.md#full)

**Read more:** [Example](./examples/GetTeamByID.md)


## Player
```
    GET /players/:playerId
```
**Description:** Returns info about Player

**Input parameters:** 

   - `playerId` -  ID of Player (required)
      
**Output:** [Player object](./definitions/Player.md#full)

**Read more:** [Example](./examples/GetPlayerByID.md)


## Territory
```
    GET /territories/:territoryId
```
**Description:** Returns info about Territory

**Input parameters:** 

   - `territoryId` -  ID of Territory (required)
      
**Output:** [Territory object](./definitions/Territory.md#full)

**Read more:** [Example](./examples/GetTerritoryByID.md)


## Updates
```
    GET /updates/?goalapi_notification_timestamp=:timestamp
```
**Description:** Returns Matches updated today. 
Also this API-call checks for updates on data of other types (Standings, Teams, etc..) happened since _goalapi_notification_timestamp_. 
Links for updated data receiving are put to Link header of response. 

**Input parameters:** 

   - `goalapi_notification_timestamp` -  Timestamp value. This API-call returns all items with lastUpdateTime greater than or equal to _goalapi_notification_timestamp_
      
**Output:** Array of [Match objects](./definitions/Match.md)

**Read more:** [How to work with Updates](./howto/Updates.md)


## Updates by Data Types
```
    GET /updates/:dataType/?goalapi_notification_timestamp=:timestamp
```
**Description:** Returns array of Matches or Standings or Teams or Tournaments or Seasons or Stages updated since _goalapi_notification_timestamp_ 
This API-call returns 128 items maximum, to get all results client must follow "next" link in _Link_ header of response 

**Input parameters:** 
   - `dataType` - One of `matches`, `standings`, `teams`, `tournaments`, `seasons`, `stages`
   - `goalapi_notification_timestamp` -  Timestamp value. This API-call returns all items with lastUpdateTime greater than or equal to _goalapi_notification_timestamp_
      
**Output:** Array of [Match objects](./definitions/Match.md) or [StandingsTable objects](./definitions/StandingsTable.md) 
or [Team objects](./definitions/Team.md) or [Tournament objects](./definitions/Tournament.md) 
or [Season objects](./definitions/Season.md) or [Stage objects](./definitions/Stage.md)

**Read more:** [How to work with Updates](./howto/Updates.md)

