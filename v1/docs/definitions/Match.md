# Match

### Properties

* `id` - String - ID of the Match

* `begin_time` - [DateTime object](./DateTime.md) - The moment when the Match is supposed to start accordingly to competition schedule
* `last_update_time` - [DateTime object](./DateTime.md) - The moment of last data update for this Match
* `status` - Hash - Current state of the Match
    - `status` - String - Current [Status](#statuses) of Match
    - `score` - Array - Array of two values indicating current score of Match
    - `finished_after` - String - If Match is finished, this field indicates the last [Period](#periods) of Match
    - `reason` - String - If Match is canceled, postponed or interrupted this field indicates the reason of abnormal Match flow
    - `period_finish_time` - [DateTime object](./DateTime.md) - If Match is online, indicates the moment when current period supposed to be finished. 
    Since we know the duration length of each period, it allows to determine current minute.  
* `tournament`- [Tournament object](./Tournament.md) - The Tournament this Match related to 
* `season`- [Season object](./Season.md) - The Season this Match is played in
* `stage`- [Stage object](./Stage.md) - The Stage this Match is played in
* `context` - Hash - Some additional data about this Match; 
    - `group` - String - Group name for Stages with groups where this Match is played  
    - `zone` - String - Zone or Conference name for competitions divided by zones or conferences
    - `matchday` - String - Match day number
    - `leg` - Number - Leg for two legged matches
        - `1` - First leg
        - `2` - Second leg
    - `round` - String - Competition round inside playoff stages
    - `final` - Number - More formal value for playoff round 
        - `1` - Final
        - `2` - Semi-final
        - `3` - Match for third place
        - `4` - Quarter-final
        - `8` - Round of 16
        - `16` - Round of 32
        - and so on
    - Other fields also possible
* `teams` - Array -  The Array containing info about Teams taking part in this Match. 
In case of match representation each Team object will contain `squad` attribute containing info about [Players Line Ups](#squad).    
    - `0` - [Team object](./Team.md) - hosts Team.
    - `1` - [Team object](./Team.md) - visitors Team
* `events`- Array of [Event objects](#event) - Events happened in this Match
* `penalty_shootout` - Hash - Details of penalty shootout (if takes place in Match)
    - `score` - Array - score of penalty shootout
    - `kicks` - Array of [Penalty Shootout Kick objects](#penalty-shootout-kick) - info about each kick


## Squad
 Squads may have 2 fields: `eleven` - array of players which starts the match on pitch and `substitutions` - array of substitution players.
 Each item of `eleven` and `substitutions` arrays is an object containing info about player and his position on pitch.   

### Properties
* `eleven` - Array of [PlayerInSquad objects](./Squad.md#player) - Players which starts the match on pitch
* `substitutions` - Array of [PlayerInSquad objects](./Squad.md#player) - Substitution players


## Event

### Properties
* `type` - String - Type of Match event; can be one of `goal`, `penalty_missed`, `card`, `substitution`
* `moment` - Hash - Moment of Match when this Event happened
    - `period` - The [Period](#periods) when this Event happened
    - `minute` - Minute of Match when this Event happened
* `team` - [Team object](./Team.md) - The Team caused this Event
* `player` - [Player object](./Player.md) - For all Events except substitutions indicates the Player caused this Event
* `players` - Hash - For Substitutions indicates the IN/OUT players
    - `in` - [Player object](./Player.md) - Player coming into the game
    - `out` - [Player object](./Player.md) - Player leaving the game 
* `score` - Array - For goal events indicates the score of Match after this goal scored
* `color` - String - For card events indicates the type of card; can be one of `yellow`, `red`, `yellow_red`
 

## Penalty Shootout Kick

### Properties
* `team` - [Team object](./Team.md) - The Team kicking the penalty
* `player` - [Player object](./Player.md) - The Player kicking the penalty
* `score` - Array - The Score after this kick
* `missed` - Boolean - True if kick is missed


## Periods
  String value. Can be one of listed below:
   - `1T`, `2T` - first and second halves of basic time    
   - `HT` - half-time break
   - `ET`, `E1T`,  `E2T` - extra-time of Match or first or second half of extra-time (if possible)  
   - `EHT` - break between two halves of extra-time
   - `PS` - penalty shootout


## Statuses
  String value. Can be one of listed below:
   - `scheduled` - Match now started yet
   - `online` - Match is playing now
   - `finished` - Match finished
   - `postponed` - Match not started in time and will be played later
   - `canceled` - Match will not be played
   - `interrupted` - Match was started, but stopped. May be replayed later, finished or canceled later
