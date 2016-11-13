
# GoalAPI Documentation Overview 
This describes the resources that make up the GoalAPI.com API. 

By default, all requests receive the **v1** version of the API. We encourage you to explicitly request this version specifying /v1 endpoint after hostname.

 - Documentation for GoalAPI-v1 in human readable format [is here](v1/docs/docs-v1.md)
 - OpenAPI (swagger) specification [is here](v1/schema/swagger.json)

All API access is over HTTP, and accessed from the `http://api.goalapi.com`. Currently **v1** supports only one media type which is _application/json_ and all responses will have `Content-Type: application/json` header. All data is sent and received as JSON.  

There is one way for authentication through GoalAPI-v1: clients must send API key inside `X-AUTH-APIKEY` header. 

