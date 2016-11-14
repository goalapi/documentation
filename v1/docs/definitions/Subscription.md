# Subscription

An object representing the state of Subscription
 

### Properties

* `apikey_md5` - String - MD5 encrypted API key
* `status` - String - **OK** means that this subscription is active, other statuses means some problems
* `blocked` - Boolean - If true, then prohibits all operations with data for current Subscription
* `expirationTime` - [DateTime](./DateTime.md) - The moment when the Subscription is no longer active
* `hasAccessToAllTournaments` - Boolean - If true and status is OK, then this subscription has access to all available Tournaments
* `allowedTournaments` - Array of [Tournament objects](./Tournament.md) - The List of tournaments available for current Subscription