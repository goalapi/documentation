# Standings Table

### Properties

* `id` - String - ID of the Table
* `tournament`- [Tournament object](./Tournament.md) - The Tournament 
* `season`- [Season object](./Season.md) - The Season 
* `stage`- [Stage object](./Stage.md) - The Stage this Standings Table belongs to
* `context` - Hash - Some additional data about this Table; 
    - `group` - String - Group name for Stages with groups  
    - `zone` - String - Zone or Conference name for competitions divided by zones or conferences
    - Other fields also possible
* `rows` - Array of [Standings Table Rows](#row) - List of Standings Table Rows representing results of the Teams


## Row 
* `team` - [Team object](./Team.md) - The Team represented by current row
* `position` - Number - Position of Team in ranking
* `points` - Number - Number of points earned by Team
* `matches` - Hash
    - `played` - Number - Number of Matches played by Team in current Stage
    - `won` - Number - Number of Matches Team has **won**
    - `draw` - Number - Number of Matches finished in **draw**
    - `lost` - Number - Number of Matches Team has **lost**
* `goals` - Hash
    - `scored` - Number - Number of goals **scored** by Team in current Stage
    - `conceded` - Number - Number of goals **scored against** this Team in current Stage
    
 
