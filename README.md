# Getting Started with the Xakia Public API

This is a quickstart guide to get you up and running with the basics of interacting with the Xakia Public API. 

The Xakia Public API is a set of HTTPS endpoints that allow you to programmatically interact with matter and intake data in a Xakia location. 

## Configuring a Location 

An API Client must be created in the desired Xakia location. This can be done by a Xakia Location Administrator by navigating to the Admin section of Xakia and selecting the "Developers" tab on the left hand side. You can then use the "Create Key" button to create an API client. 

The page will display the following information when you create and API client:

  * Client Name: this is a name that can be used to refer to the API client. 
  * Client id: this is an OAuth 2.0 client ID that identifies the API client.
  * Secret 1 and Secret 2: These are OAuth 2.0 client secrets that can be used to obtain access tokens. 

Note that the secret values are only shown to you once, when they are first generated. If you navigate away from the page and then come back, the secret values will be hidden from you and you will not be able to record them. Ensure that you record the secret values when they are first generated. 

You can regenerate the secret values at any time. Note that when you regenerate a secret value, the old value for the secret is invalidated and can no longer be used to obtain access tokens. 

Note that there are two client secrets provided. Either client secret can be used to obtain access tokens, and both are valid at the same time. The reason that two are provided is to allow your application to cycle a secret with zero downtime. For example - say your application is using Secret 1, and you want to generate a new value for Secret 1. You can change your application to use Secret 2, then re-generate Secret 1, then change your application to use the new value for Secret 1. This process thusly rotates the secret value without ever being unable to authenticate to Xakia. 

The page also shows some header values that you need to use to call the Xakia API:

  * x-xa-tenant - this value identifies the tenant or company that your application is trying to access.
  * x-xa-location - this value identifies the company location that your application is trying to access. 

## Authentication

The Xakia Public API uses OAuth 2.0 with JWT bearer tokens. Clients obtain access tokens from the Xakia token server and then present the access token with each API request. 

To obtain an access token, you need to use the OAuth 2.0 client credentials flow with the client id and client secret provided in the steps above. 

For example, you can use the following HTTPS request to obtain an access token:

```
POST https://login.xakiatech.com/connect/token

Content-Type: application/x-www-form-urlencoded

client_id=<your-client-id>&
client_secret=<your-client-secret>&
grant_type=client_credentials 
```

The response will include an access token. 

When calling a Xakia Public API endpoint, always provide the following headers:

x-xa-tenant: <tenant ID from the API Key page>
x-xa-location: <location ID from the API Key page>
x-xa-region: <one of AU, US, UK or CA, depending on the region you are accessing>
Authorization: Bearer <your access token>
  
## Browsing the API 

The Xakia Public API provides an OpenAPI 3 compliant definition with a Swagger UI that can be used to browse the available API endpoints. This can be found here: https://xapi-au.xakiatech.com/apibrowser/index.html  . Note that the API browser endpoints are region specific - you will need to use xapi-au.xakiatech.com for AU locations, xapi-us.xakiatech.com for US locations, etc. 

The API browser will also allow you to interact with the API directly. Use the "Authenticate" button to enter your access token, and then ensure to supply the location, tenant and region headers on each request. 

## Support 

For any queries about the Xakia Public API please email support@xakiatech.com . 

  


