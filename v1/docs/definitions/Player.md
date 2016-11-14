# Player

### Properties

* `id` - String - ID of the Player
* `name` - String - Name of Player
* `country` - [Territory object](./Territory.md) - Country of Player
* `position` - String - Position of Player on pitch; can be `goalkeeper`, `defender`, `midfielder`, `forward` or `player`
* `names` - Hash - Player name variants
    - `short` - String - Short writing of Player's name
    - `full` - String - Full name of Player
    - `first` - String - First name of Player
    - `second` - String - Second name of Player
* `bio` - [Hash](#biometrics) - Some additional data about player, biometrics, etc...  
    - `birth-date` - String - Birth date of Player
    - `birth-country` - String - Birth country of Player
    - `weight` - String - Weight of Player
    - `height` - String - Height of Player
