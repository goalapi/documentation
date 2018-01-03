# Push Updates / Data Update Notifications
In context of API described in this documentation, **Push Updates** mean not more than that the *Service* is able to notify
 consumers about updates in data they are interested in. **Push** term is used as an antonym for **Pull**. 
 It's not **PUSH-method** of HTTP requests nor **PUSH notifications** used in mobile apps, while the general meaning is very close.
 In short, it means that client should not poll the service with recurring requests each **N seconds/minutes**, instead of it, 
 the client is offered to develop and register a *Listener* which will receive *Notification* about data updates.   

## Listener application and Notifications 
The *Listener* is a web-application available via static URL. The purpose of *Listener* is to process *Notifications* 
sent from *Service*. *Notifications* are HTTP-requests sent with **GET** method. *Notifications* do not contain updated data itself. 
The only useful content of *Notification* is **goalapi_notification_timestamp** query parameter, which contains UNIX timestamp 
representation of moment which updates taken from. 

**Example:**
```
    http://your.server.url/your/listener.app?goalapi_notification_timestamp=1469560782
```

As soon as the *Listener* is registered, the service sends *Notifications* about updates happened after the moment of 
registration. If particular *Notification* is successfully processed by *Listener*, the *Service* won't repeat it again
and will "focus" on next upcoming data updates. Two major points in updates processing workflow is that the **GET** request 
is sent from the *Service* to *Listener* and *Listener* sends result of notification processing in response. 

The indicator of successful result is **200 OK** response code. 
Though no strict rules on how to get updates, the best practise is to utilize [Updates API](./howto/Updates.md). 
In your *Listener* it's recommended to implement workflow described below
 
### Updates Notification processing workflow
After  *Listener* receives *Notification*
 1. *Listener* extracts **goalapi_notification_timestamp** parameter from QUERY STRING part of request
 1. *Listener* sends **Updates API-call** to see what data updated (`http://api.goalapi.com/v1/updates/?goalapi_notification_timestamp=GOALAPI_NOTIFICATION_TIMESTAMP_VALUE`)
 1. *Listener* extracts and parses value of **Link** header of response received ar previous step
 1. For each Link item parsed above *Listener* sends API-call to receive appropriate datum (it can be Matches, Standings and objects of other types)
 1. Keep possible [pagination](./howto/Updates.md#Pagination) in mind for results fetched at previous step
 1. After all updates received and saved, send **200 OK** HTTP-response
 
### Listener failures
Sometimes it's possible that the *Service* is not able to deliver *Notification* to *Listener* due to connectivity problems 
or other problems which may happen on both sides. 
After 5 failures of particular *Listener*, the *Service* will stop sending of *Notifications* until it's reactivated.
Reactivation is performed after *Listener* becomes available again and sends **200 OK** response for **PING** request sent from the *Service*.
**PING** is the GET request sent to the same address as regular *Notification*, but with `&ping=1` parameter in query string.
The *Listener* should not do anything except responding with **200 OK** status when request with `&ping=1` is received. 
