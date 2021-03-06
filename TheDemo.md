# OIDC Auth API Demo

The demo intends to show the a standard OIDC/OAuth Authorisation code flow.

Here's the architecture:

![Demo Architecture](https://github.com/andywillmot/Reboot2020/blob/master/architecture.png "Demo architecture")

## Pre-requisites
1) Python 3
2) Nodejs


## The Identity Provider - set this up first so you have your config settings

I've used Auth0, mainly because they have a lot of good tutorials on their website.  But I coud have used Google or served a local one through Docker (There's a few on DockerHub).  Basically you just need to register and setup an App for authentication, plus an API for access.  Here's the setup: [How to setup Auth0 as an IDP](https://github.com/andywillmot/Reboot2020/blob/master/creating-the-idp.md)

## The client

Have based the client on the Auth0 react samples here: https://github.com/auth0-samples/auth0-react-samples/tree/master/02-Calling-an-API

There's a step-by-step tutorial here: https://github.com/auth0-samples/auth0-react-samples/tree/master/02-Calling-an-API

Or have a look at [how to build the client](creating-the-client.md) to get going with this demo quickly.

## The server

This is based on Django's (a python web framework) Rest Framework.  It doesn't do much other than return a json string on failure/success.
You can get this going quickly by working through [how to build the server](creating-the-server.md), but you may want to put you're own API endpoint here. 

## Testing

So if you followed the guides OK (and I didn't make any mistakes), you now should have:
1) An OIDC compliant IDP via Auth0
2) A react client app served through http://localhost:3000
3) A Django-based authenticated API served through http://localhost:8000/api/private

You now should be able to "Login" from the client whereby you'll be redirected to an Auth0 login page.  Login with your user you setup for the IDP.  You should be redirected back to the client app where you then should be able to client on External API and ping the endpoint to return a successful response. 

Introspect the JWT access token returned with Chrome Dev Tools by finding it in the Auth0 response and using https://JWT.io to decode. 
