# Reboot2020 - OIDC/OAuth Lightning talk

GitHub link:
![GitHub QR Code](https://github.com/andywillmot/Reboot2020/blob/master/QRCode.png "https://github.com/andywillmot/Reboot2020/")

## Definitions - It's all pretty clear!
### OAuth
>An open standard for **access delegation**, commonly used as a way for Internet users to grant websites or applications access to their information on other websites but without giving them the passwords.
### OIDC (OpenID Connect)
>An open standard and decentralized **authentication** protocol promoted by the non-profit OpenID Foundation.  The lastest standard is OpenID Connect 1.0, created as an extension of OAuth 2.0.

![Confused chicken...](https://github.com/andywillmot/Reboot2020/blob/master/confused-chicken.jpg "I'm a bit confused chicken!")
I'm a bit confused chicken.



## A slightly simplistic but 'good enough' way to think about it....
### Authorisation
>The act of giving permission - This is what **OAuth** does
### Authentication
>The act of verifying the identity of a user - This is what **OIDC** extends OAuth to do


## Understanding the history helps

![History](https://github.com/andywillmot/Reboot2020/blob/master/history.jpg "OpenID & OAuth history")

## How the standards work together ##

![Standards map](https://github.com/andywillmot/Reboot2020/blob/master/OpenIDConnect-Map-4Feb2014.png "Standards Map")

## What are the key concepts? ##

### Tokens ###
There are a few types of tokens to be aware of.  API Keys, MAC Tokens for example.  But, for the purposes of OIDC/OAuth we use "Bearer" tokens:

**Bearer tokens**
>A Base64 string of characters used by the bearer (the client) to access a resource provided by a resource owner.   

They can be either:
* a meaningless string
* a JSON string of data called a JWT (or "jot") based on the open standard RFC 7519, which can be signed into a JWS and/or encrypted into a JWE

#### Here's what a JWT looks like ####

```javascript
{
  "alg": "HS256",
  "typ": "JWT"
}
.
{
  "sub": "1234567890",
  "name": "John Doe",
  "admin": true
}
.
HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  secret)
```

Which, for transmission, would get BASE64 encoded to:

```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWV9.TJVA95OrM7E2cBab30RMHrHDcEfxjoYZgeFONFh7HgQ
```
### How do we use bearer tokens in OAuth ###
In OAuth 2.0 there are three types of *bearer token*:
1) **Authorisation token** - provided on a succesful authentication and used to obtain an access token
2) **Access token** - used to gain access to a resource
3) **Refresh token** - sometimes received with an access token and used to get a new access token when the previous one has expired 

And OIDC 1.0 introduces another token:
4) **Identity token** - used to described information about the identity of the user

## Grants ###
Defined in OAuth, *grants* define the type of token scheme used for the authorisation process. In OAuth 2.0 there is:
1) **Authorisation Code grant** - request an authorisation token via a redirect, then use this to request an access token
2) **Implicit grant** - request an access token via a redirect
3) **Resource Owner Password Credential grant** - client gets credentials from resource owner, then uses these to request an access token.  Used where the resource owner trusts the client.
4) **Client Credential grant** - client reqests an access token using their own credentials

## Flows ##
While *flows* are mentioned in OAuth 2.0, OIDC 1.0 fully defines a set of flows based around OAuth grants:
1) **Authorisation code flow** - Basically the authorisation code grant, but with some extra bells on
2) **Implicit flow** - Basically the implicit grant, but with some extra bells
3) **Hybrid flow** - A combination of authorisation code and implicit grant, with even more bells on

## Scopes ##
*Scopes* provide a method to limit access to a resource for a client, making the authorisation more granular than normal session-based authorisation.  
Scopes are mentioned in OAuth 2.0, but OIDC makes this real by providing a number of built in ones.  For example:
* **profile** - requests access to default profile claims
* **email** - requests access to email and email_verified claims
* **address** - requests access to address claim
* **phone** - requests access to phone_number and phone_number_verified claims

## Claims ##
*Claims* are an OIDC concept.  They define the granular "thing" claimed by the client, within the scope requested. For example, the profile scope has these and more:
* name
* family_name
* given_name
* middle_name
* nickname
* preferred_username

## Response Types ##
The *response_type* is an OAuth defined field used to request a particular token grant.  OIDC extends this to request a particular authentication flow.  
OAuth response_types:
* **code** - Authorisation code grant
* **token** - Implicit grant

OIDC extra response types:
* id_token
* id_token token
* code id_token
* code token
* code id_token token
* none

Note, *response_types* and *scopes* can be mixed and matched.  E.g. you can have an OAuth response_type with an OIDC scope.

This excellent post on medium describes each of these response types in detail:  
https://medium.com/@darutk/diagrams-of-all-the-openid-connect-flows-6968e3990660

## Bringing them all together ##
So, here are the auth options that OIDC/OAuth provides. It gets complicated so this may not be all correct!

| Specification | OIDC Flow | OAuth Authorization grant | response_type | OIDC scope? | /authorize response | /token reponse |
|-----------|-----------|--------------------------------------|---------------------|-------------------------|----------------------|--------------------|
| OAuth 2.0 | Auth code | Auth code | code | no | Auth token | Access token |
| OAuth 2.0 | Implicit | Implicit | token | - | Access token | not used |
| OAuth 2.0 | n/a | Resource Owner  Password Credentials | - | no | not used | Access token |
| OAuth 2.0 | n/a | Client Credentials | - | no | not used | Access token |
| **OIDC 1.0** | **Auth code** | **Auth code** | **code** | **yes** | **Auth token** | **ID & Access tokens** |
| OIDC 1.0 | Implicit | Implicit | id_token | - | ID token | not used |
| OIDC 1.0 | Implicit | Implicit | id_token token | - | ID & Access tokens | not used |
| OIDC 1.0 | Hybrid | Auth code | code id_token | - | ID & Auth tokens | ID & Access tokens |
| OIDC 1.0 | Hybrid | Auth code & Implicit | code token | yes | Auth & Access tokens | ID & Access tokens |
| OIDC 1.0 | Hybrid | Auth code & Implicit | code token | no | Auth & Access tokens | Access token |
| OIDC 1.0 | Hybrid | Auth code & Implicit | code id_token token | - | ID, Auth & Access  | ID & Access tokens |
| OIDC 1.0 | n/a | n/a | none | - | none | none |

Note, for the demo we're going to use the one in bold - OAuth's Auth code grant with OIDC scope extension. 

## Sources ##

https://scotch.io/tutorials/the-anatomy-of-a-json-web-token
https://jwt.io/
https://developer.okta.com/blog/2017/07/25/oidc-primer-part-1
https://medium.com/@darutk/diagrams-of-all-the-openid-connect-flows-6968e3990660



