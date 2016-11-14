# Squad

### Properties

* `id` - String - ID of the Team
* `name` - String - Title of Team
* `tournament`- [Tournament object](./Tournament.md) - The Tournament this Stage belongs to
* `season`- [Season object](./Season.md) - The Season this Squad played in
* `stage`- [Stage object](./Stage.md) - The Stage this Squad played in
* `players` - Array of [PlayerInSquad objects](#player) - Players of Team played in specified Season or Stage


## Player

### Properties

* `id` - String - ID of the Player
* `name` - String - Name of Player
* `position` - String - Position of Player on pitch; can be `goalkeeper`, `defender`, `midfielder`, `forward` or `player`
* `number` - Number - Shirt number of player
* `captain` - Boolean - Indicates if current Player is a captain of Team
